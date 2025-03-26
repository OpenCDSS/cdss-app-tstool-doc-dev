# TSTool / Software Design / Java Runtime Environment #

This documentation focuses on technical issues related to the Java Runtime Environment.

*   [Java Language](#java-language)
*   [Java Runtime Environment (JRE)](#java-runtime-environment_1)
*   [64-bit and 32-bit Versions](#64-bit-and-32-bit-versions)
*   [Java Launcher](#java-launcher)
*   [Classpath](#classpath)
*   [Plugins and Class Loaders](#plugins-and-class-loaders)

--------------

## Java Language ##

TSTool is written in the Java language, with use of C or other languages only when used by third-party components.
The TSTool [`RunPython`](https://opencdss.state.co.us/tstool/latest/doc-user/command-ref/RunPython/RunPython/)
command does allow integrating Python and TSTool/Java and future TSTool releases may further support this approach,
but languages other than Java are not currently used for primary functionality.
Java source code consists of files with `*.java` filename extension.
Code files include classes, interfaces, enumerations, etc.
The source code is compiled into bytecode in class files with `*.class` filename extension.
These files are directly used in the development environment to run TSTool and are
packaged into Java Archive (`*.jar`) files for distribution and use at run-time.

## Java Runtime Environment ##

A [Java Runtime Environment (JRE)](../../resources.md#java) that is the same or newer than the Java version used in the development environment
is required to run TSTool in the operational environment.
For example, TSTool developed and distributed with Java 11 cannot be run using JRE 8.
A newer version of Java runtime can run an older version of compiled java code.
Although it is possible to rely on a Java version on the computer, TSTool software is distributed with its own JRE.

See the `jre_VERSION` folder under the TSTool installation,
for example:

*   `jre_11` when Java 11 is used
*   `jre_18` when Java 8 is used
    (this convention of using 1.8 for Java 8 and eearlier is from Java and was changed after Java 8)

The JRE allows Java to be run in a protected virtual environment separate from other Java installations on the computer.

## Java Launcher ##

The JRE is runs TSTool via a TSTool launcher program.
On Windows, the open source [Launch4J](../../resources.md#launch4j)
software is used to run TSTool.

On Linux the `tstool` script is used.

## 64-bit and 32-bit Versions ##

As of TSTool version 14.0.0, 64-bit java is used for development and runtime libraries.

TSTool prior to version 14.0.0 uses 32-bit java,
which supports components that use native Windows 32-bit libraries,
in particular the HEC-DSS libraries.

TSTool has been updated to use 64-bit Java for development and runtime.
There are no longer any HEC-DSS limitations.

## Classpath ##

The JRE starts by specifying the class path to look for `*.class` and `*.jar` files in the installation `bin/` folder.

## Plugins and Class Loaders ##

TSTool 12.x is beginning to support plugin datastores and commands.
This requires that the JRE is able to dynamically load code from plugin jar files.
It also is helpful to isolate such plugin files from the main distribution.
Determining the best way to support plugins is an area of active research and development.
New features in Java 9 may simplify plugin implementation.
However, Java 9 is not currently being used as of TSTool 12.x.
See also:

*   [Plugin Commands](../plugin-commands/plugin-commands.md)
*   [Plugin Datastores](../plugin-datastores/plugin-datastores.md)
