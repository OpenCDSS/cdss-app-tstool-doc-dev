# Java Runtime Environment #

This documentation focuses on technical issues related to the Java Runtime Environment.

* [Java Language](#java-language)
* [Java Runtime Environment (JRE)](#java-runtime-environment_1)
* [32-bit and 64-bit Versions](#32-bit-and-64-bit-versions)
* [Java Launcher](#java-launcher)
* [Classpath](#classpath)
* [Plugins and Class Loaders](#plugins-and-class-loaders)

--------------

## Java Language ##

TSTool is written in the Java language, with use of C or other languages only when used by third-party components.
The TSTool [`RunPython`](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/RunPython/RunPython/)
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
For example, TSTool developed and distributed with Java 8 cannot be run using JRE 7.
Although it is possible to rely on a Java version on the computer, TSTool software
is distributed with its own JRE.  See the `jre_VERSION` folder under the TSTool installation,
for example `jre_18` when Java 8 is used (the convention of using 1.8 for Java 7, etc. is from Java developers
and TSTool conventions need to migrate to the more easily understood "8" as time allows to make this change).
The JRE allows Java to be run in a protected virtual environment separate from other Java installations on the computer.

## Java Launcher ##

The JRE is runs TSTool via a TSTool launcher program.
On Windows, the open source [Launch4J](../../resources.md#launch4j)
software is used to run TSTool.

On Linux the `tstool` script is used.

## 32-bit and 64-bit Versions ##

As of TSTool version 12.x, 32-bit java is used because some components use native Windows 32-bit libraries,
in particular the HEC-DSS libraries.
Additional effort is needed to support 32- and 64-bit versions in the development and deployed environment.
It is possible to replace the deployed JRE with alternate version by replacing
the `jre_VERSION` folder with a different version of Java.

## Classpath ##

The JRE starts by specifying the class path to files and folders with `*.class` and `*.jar` file extension.
The current approach taken in TSTool is to exactly specify files to load, rather than just the
folder where to search for files.
This may be changed to specify the folder, so that startup can be simpler.
However, this increases the opportunity for errors if extra files have somehow been added to the folder.
See also the next section on plugins.

## Plugins and Class Loaders ##

TSTool 12.x is beginning to support plugin datastores and commands.
This requires that the JRE is able to dynamically load code from plugin jar files.
It also is helpful to isolate such plugin files from the main distribution.
Determining the best way to support plugins is an area of active research and development.
New features in Java 9 may simplify plugin implementation.
However, Java 9 is not currently being used as of TSTool 12.x.
See also:

* [Plugin Commands](../plugin-commands/plugin-commands.md)
* [Plugin Datastores](../plugin-datastores/plugin-datastores.md)
