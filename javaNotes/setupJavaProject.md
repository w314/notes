maven, java

# Create Java Porject

## Install

### [Installation](https://www.digitalocean.com/community/tutorials/install-maven-linux-ubuntu)

#### Step 1: Download the JDK Binaries

Go to the [URL](https://jdk.java.net/20/), copy the download link for Linux/x64 build ending `linux-x64_bin.tar.gz`. Then use the below command to download and extract it.

```bash
$ wget https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1_linux-x64_bin.tar.gz
$ tar -xvf openjdk-20.0.1_linux-x64_bin.tar.gz
$ sudo mv jdk-20.0.1 /opt/
```

I have moved JDK to /opt, you can keep it anywhere in the file system.

#### Step 2: Setting JAVA_HOME and Path Environment Variables

Open .profile file from the home directory and add the following lines to it.

```bash
JAVA_HOME='/opt/jdk-20.0.1'
PATH="$JAVA_HOME/bin:$PATH"
export PATH
```

You can relaunch the terminal or execute `source .profile` command to apply the configuration changes.

#### Step 3: Verify the Java Installation

You can run `java -version` command to verify the JDK installation.

### Install `Maven`

#### Step 1: Download the Maven Binaries

Go to [maven](https://maven.apache.org/download.cgi). Copy the link for the `Binary tar.gz archive` file. Then run the following commands to download and untar it.

```bash
$ wget https://dlcdn.apache.org/maven/maven-3/3.9.3/binaries/apache-maven-3.9.3-bin.tar.gz
$ tar -xvf apache-maven-3.9.3-bin.tar.gz
$ sudo mv apache-maven-3.9.3 /opt/
```

#### Step 2: Setting M2_HOME and Path Variables

Add the following lines to the user profile file (.profile).

```bash
M2_HOME='/opt/apache-maven-3.9.3'
PATH="$M2_HOME/bin:$PATH"
export PATH
```

Relaunch the terminal or execute `source .profile` to apply the changes.

#### Step 3: Verify the Maven installation

Execute `mvn -version` command and it should produce the following output.

## Project Setup

### Create Project

In `vsCode`have extension pack for java installed in vsCode then:

- CTRL + SHIFT + P
- select `Maven: Create Maven Project`
- The "Do you want to select an archetype?" means do you want to use a template? for simple test project select `no Archetype`
- `group id` is basically the company you work for like: com.wp
- `artifact id` is the project name: like tryout
- select destination folder for project and maven creates project folder

### Start Project

- open project folder in VSCode
- update `JRE` version to the one used is there is a warning about it
- run `mvn validate`, should be successfull

```bash
# validates correct maven project
mvn validate
```

To avoid `no manifest attribute` at the build phase:

- configure `pom.xml`, add `maven-assembly-plugin` to `<build>` tag
- under `<configuration>` add `<archive>` tag with the location of the `main` method

```xml
<build>
  <plugins>
    <plugin>
      <artifactId>maven-assembly-plugin</artifactId>
      <version>3.6.0</version>
      <configuration>
        <descriptorRefs>
          <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
        <!-- Add location of main file -->
        <archive>
          <manifest>
            <mainClass>com.wp.Main</mainClass>
          </manifest>
        </archive>
      </configuration>
      <executions>
        <execution>
          <id>make-assembly</id> <!-- this is used for inheritance merges -->
          <phase>package</phase> <!-- bind to the packaging phase -->
          <goals>
            <goal>single</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

Run:

```bash
# creates .class files under target/classes
mvn compile
# runs unit tests, there will be none for now
mvn test
# creates jar file under target
mvn package
# can be run by
java -jar ./target/myJarFile.jar
```

Your project will output "Hello world!" in the terminal.

### Setup Git Repository

```bash
git init
git add .
git commit -m 'Intial commit'
```

Create remote repository and add it to project:

```bash
git remote add origin <remote-directory-url>
git push --set-upstream origin master
```
