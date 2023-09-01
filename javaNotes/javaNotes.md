## Maven

> What is Maven? Why would we use it?

`Maven` is a tool that can be used for building and managing any Java-based project.

We use it as Maven helps in:

- Simplifying the build process
- Adding jars and dependencies
- Documenting project information with change logs and reports
- Integration with source control systems (Git)

Maven project configuration and dependencies are handled via the `Project Object Model`, defined in the `pom.xml` file. This file contains information about the project, is used to build the project, includes project dependencies and plugins.

Some important tags within the pom.xml file include:

- `<project>` - this is the root tag of the file
- `<modelVersion>` - defining which version of the page object model to be used
- `<name>` - name of the project
- `<properties>` - project-specific settings
- `<dependencies>` - this is where you put your Java dependencies you want to use. Each one needs a `<dependency>`, which has:
  - `<groupId>`
  - `<artifactId>`
  - `<version>`
- `<plugins>` - for 3rd party plugins that work with Maven
