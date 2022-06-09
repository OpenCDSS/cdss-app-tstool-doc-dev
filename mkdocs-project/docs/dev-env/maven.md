# TSTool / Development Environment / Maven ##

Maven software is used to manage software library dependencies.

This documentation was updated on 2022-05-28 for Maven 3.8.5.

* [Introduction](#introduction)
* [Maven Installation](#maven-installation)
    + [Maven Installation on Windows](#maven-installation-on-windows)
* [Automating Tasks with Maven](#automating-tasks-with-maven)
    + [Listing a Project's Dependencies](#listing-a-projects-dependencies)

----

## Introduction ##

Maven software manages Java dependencies and build processes is used by newer software projects.
Newer TSTool projects such as plugins use Maven.
TSTool projects will be converted to Maven as resources allow.
Maven is similar to dependency tools in other languages such as `npm` for JavaScript.
TSTool software has in the past included libraries by including library `jar` files in a project's
`lib` folder and specifically included the `jar` file in the class path using the Eclipse project's ***Build Path*** settings.
The `jar` files are committed to the repository.

In contrast, Maven uses a library repository to manage library dependencies.
For Maven version 2, the repository is a folder named `.m2/repository` in the user's files,
and subfolders containing `jar` files for different dependency versions,
where folders match the Java package folders.
A project's dependencies and other configuration information is defined in a Project Object Model (`pom.xml`) file,
which is located in the Maven project's main folder.

Until all TSTool projects are converted to Maven,
care must be taken to package `jar` files for the deployed software.

Maven is an alternative to Ant software.
Both Ant and Maven are integrated with Eclipse.

In addition to the dependency repository,
Maven software can be installed independent of Eclipse to perform software project tasks on the command line,
such as creating scripts to automate plugin installers.
The Maven version integrated with Eclipse is typically an older version than the latest Maven software
and care must be taken to confirm that the Eclipse project's `pom.xml` can be used consistently with Eclipse.
Otherwise, it may be necessary to update the Eclipse version and/or Eclipse Maven plugin.

## Maven Installation ##

Maven is installed from a `zip` file on Windows and `tar` file on Linux.
See the [Apache Maven Project download page](https://maven.apache.org/download.cgi).

### Maven Installation on Windows ###

Install Maven on Windows by following the instructions on the installation page.
This involves unzipping the `*bin.zip` file into a folder such as `C:\Program Files\Maven\apache-maven-3.8.5\`
and setting the `PATH` environment variable to resulting `bin` folder.
The `mvn` program can then be run on the command line
using a Windows `cmd` shell, Git Bash shell, etc.
A new command shell must be opened in order to recognize the change to the `PATH`.

It may also be possible to install Maven within Git Bash MinGW environment or Cygwin rather than Windows;
however, this approach is not documented here.

Once the software is installed and the `PATH` is configured, confirm by running the following in Git Bash or equivalent:

```
which mvn

mvn --version
```

The software requires that the `JAVA_HOME` environment variable is set so that Maven knows which Java runtime environment to use.
The value should be the folder above the `bin` folder.

The `mvn` program when run may automatically install additional dependencies necessary to run a command,
and those dependencies are stored in the Maven repository.

## Automating Tasks with Maven ##

Once Maven software is installed, the `mvn` program can be used to automate tasks, such as by calling from Bash scripts.
If the `JAVA_HOME` environment is not set for the user's environment,
it will need to be set in the script.

### Listing a Project's Dependencies ###

It is useful to list the dependencies for a project, for example when building an installer for a plugin.
The following will list a dependency tree for a project, showing package names.
The command should be run in a folder where `pom.xml` file exists.

```
mvn dependency:tree -Dverbose
```

The following examples will build the class path string used by JRE.
The second example splits the class path into a separate list of `jar` files.

```
mvn dependency:build-classpath

mvn dependency:build-classpath | grep ':' | grep ';' | tr ';' '\n'
```

Example output for the TSTool AWS plugin is as follows.

```
 mvn dependency:build-classpath | grep ':' | grep ';' | tr ';' '\n'
C:\Users\sam\.m2\repository\junit\junit\3.8.1\junit-3.8.1.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\cloudfront\2.17.198\cloudfront-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\aws-xml-protocol\2.17.198\aws-xml-protocol-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\aws-query-protocol\2.17.198\aws-query-protocol-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\protocol-core\2.17.198\protocol-core-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\sdk-core\2.17.198\sdk-core-2.17.198.jar
C:\Users\sam\.m2\repository\org\slf4j\slf4j-api\1.7.30\slf4j-api-1.7.30.jar
C:\Users\sam\.m2\repository\org\reactivestreams\reactive-streams\1.0.3\reactive-streams-1.0.3.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\auth\2.17.198\auth-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\json-utils\2.17.198\json-utils-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\third-party-jackson-core\2.17.198\third-party-jackson-core-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\eventstream\eventstream\1.0.1\eventstream-1.0.1.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\http-client-spi\2.17.198\http-client-spi-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\regions\2.17.198\regions-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\annotations\2.17.198\annotations-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\utils\2.17.198\utils-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\aws-core\2.17.198\aws-core-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\metrics-spi\2.17.198\metrics-spi-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\apache-client\2.17.198\apache-client-2.17.198.jar
C:\Users\sam\.m2\repository\org\apache\httpcomponents\httpclient\4.5.13\httpclient-4.5.13.jar
C:\Users\sam\.m2\repository\commons-logging\commons-logging\1.2\commons-logging-1.2.jar
C:\Users\sam\.m2\repository\commons-codec\commons-codec\1.11\commons-codec-1.11.jar
C:\Users\sam\.m2\repository\org\apache\httpcomponents\httpcore\4.4.13\httpcore-4.4.13.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\netty-nio-client\2.17.198\netty-nio-client-2.17.198.jar
C:\Users\sam\.m2\repository\io\netty\netty-codec-http\4.1.77.Final\netty-codec-http-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-codec-http2\4.1.77.Final\netty-codec-http2-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-codec\4.1.77.Final\netty-codec-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-transport\4.1.77.Final\netty-transport-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-resolver\4.1.77.Final\netty-resolver-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-common\4.1.77.Final\netty-common-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-buffer\4.1.77.Final\netty-buffer-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-handler\4.1.77.Final\netty-handler-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-transport-classes-epoll\4.1.77.Final\netty-transport-classes-epoll-4.1.77.Final.jar
C:\Users\sam\.m2\repository\io\netty\netty-transport-native-unix-common\4.1.77.Final\netty-transport-native-unix-common-4.1.77.Final.jar
C:\Users\sam\.m2\repository\com\typesafe\netty\netty-reactive-streams-http\2.0.5\netty-reactive-streams-http-2.0.5.jar
C:\Users\sam\.m2\repository\com\typesafe\netty\netty-reactive-streams\2.0.5\netty-reactive-streams-2.0.5.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\s3\2.17.198\s3-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\arns\2.17.198\arns-2.17.198.jar
C:\Users\sam\.m2\repository\software\amazon\awssdk\profiles\2.17.198\profiles-2.17.198.jar
```

Packages that are clearly unique will not conflict with existing TSTool built-in `jar` files in the installer,
which are located in the TSTool `bin` folder when installed.
However, `jar` files that conflict with built-in `jar` files must be deployed in the plugin `dep` folder (for dependency)
and the plugin software design must use a class loader that finds the plugin-specific dependency first only for the plugin,
and the other library version for the other TSTool code.
Plugin dependency conflict is a continuing area of refinement for TSTool development.
One approach to avoiding conflicts is to review dependencies and make sure that TSTool's built-in `jar` files are the same version.
Consequently, plugins can drive updates in the TSTool main program.

The following table summarizes packages and potential conflicts in TSTool,
as of an analysis of TSTool version 14.3.

| **Package&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;** | **Jar File&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;** | **Comment** |
| -- | -- | -- |
| `software.amazon.awssdk.*` | Various | Used with [Amazon web services](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/get-started.html), unlikely to be used in other TSTool dependencies. |
| `org.lsf4j.slf4j-api.*` | `sl4j-api-*.jar` | [Logging library](https://www.slf4j.org/) that may also be used elsewhere in TSTool. |
| `org.reactivestreams.*` | `reactive-streams-*.jar` | [Library](https://www.reactive-streams.org/) to support asynchronous stream processing, used by AWS code and currently unlikely to be used elsewhere in TSTool. |
| `org.apache.*` and `commons*` | Various | Used with Apache projects for logging and other common tasks, likely to be used in other TSTool dependencies. |
| `io.netty.*` and `com.typesafew.*` | `*netty.*` | [Library](https://netty.io) for asynchronous event-driven network applications, used by AWS and currently unlikely to be used in other TSTool code or dependencies. |
