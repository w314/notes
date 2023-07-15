maven, java

# `Maven`

## [Installation](https://www.digitalocean.com/community/tutorials/install-maven-linux-ubuntu)

### Install JDK

#### Step 1: Download the JDK Binaries

Go to the [URL](https://www.oracle.com/java/technologies/downloads/), copy the download link for Linux/x64 build ending `linux-x64_bin.tar.gz`. Then use the below command to download and extract it.

```bash
$ wget https://download.oracle.com/java/20/latest/jdk-20_linux-x64_bin.tar.gz
$ tar -xvf jdk-20_linux-x64_bin.tar.gz
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

## Create Project

Have extension pack for java installed in vsCode.

OR in terminal run:

```bash
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```
