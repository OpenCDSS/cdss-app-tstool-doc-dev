# TSTool / Software Design / Overview

This page focuses on major TSTool software design topics.
The documentation will be filled out once more fundamental documentation is completed.

* [GitHub Repositories and Code Projects](#github-repositories-and-code-projects)
* [Command File and Command Syntax](#command-file-and-command-syntax)
* [Java Runtime Environment ](#java-runtime-environment)
* [Command Processor](#command-processor)
* [Command Factory](#command-factory)
* [Command Interface and AbstractCommand Class](#command-interface-and-abstractcommand-class)
* [Plugin Commands](#plugin-commands)
* [CommandStatus Class](#commandstatus-class)
* [Utility Packages](#utility-packages)
* [Logging](#logging)
* [Time Series Package](#time-series-package)
* [Datastores](#datastores)
* [Main TSTool Application](#main-tstool-application)
* [Built-in Test Framework](#built-in-test-framework)
* [Future Design Elements](#future-design-elements)

-------------------

## GitHub Repositories and Code Projects ##

The TSTool software is currently developed as multiple projects within an Eclipse workspace,
where each Eclipse project corresponds to a similarly named Git repository.
The decision about what content lives in a repository has been made based on years
of experience sharing repositories and implementing development environments.
The following table summarizes the repositories for TSTool.
A naming convention has been adopted that delineates application, library, and utility components.
This convention should allow code to be developed using environments other than Eclipse.
The Java packages within each repository have historical significance and could benefit from
refactoring; however, this will be disruptive and is not planned for the near-term.

**<p style="text-align: center;">
TSTool GitHub Repositories and Code Projects (listed alphabetically)
</p>**

|**GitHub Repository**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|**Eclipse Project**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|**Primary File Type**|**Description**|
|--|--|--|--|
|[`cdss-app-tstool-doc`](https://github.com/OpenWaterFoundation/cdss-app-tstool-doc)|`cdss-app-tstool-doc`|Word and PDF|Legacy user documentation, some developer documentation|
|[`cdss-app-tstool-doc-dev`](https://github.com/OpenWaterFoundation/cdss-app-tstool-doc-dev)|`cdss-app-tstool-doc-dev`|Markdown|New Markdown/MkDocs developer documentation|
|[`cdss-app-tstool-doc-user`](https://github.com/OpenWaterFoundation/cdss-app-tstool-doc-user)|`cdss-app-tstool-doc-user`|Markdown|New Markdown/MkDocs user documentation|
|[`cdss-app-tstool-main`](https://github.com/OpenWaterFoundation/cdss-app-tstool-main)|`cdss-app-tstool-main`|Java|Main TSTool application code|
|[`cdss-app-tstool-test`](https://github.com/OpenWaterFoundation/cdss-app-tstool-test)|`cdss-app-tstool-test`|TSTool command files|Functional tests using built-in test features.|
|[`cdss-lib-cdss-java`](https://github.com/OpenWaterFoundation/cdss-lib-cdss-java)|`cdss-lib-cdss-java`|Java|CDSS code components shared across CDSS applications|
|[`cdss-lib-common-java`](https://github.com/OpenWaterFoundation/cdss-lib-common-java)|`cdss-lib-common-java`|Java|Utility code components shared across applications|
|[`cdss-lib-dmi-hydrobase-java`](https://github.com/OpenWaterFoundation/cdss-lib-dmi-hydrobase-java)|`cdss-lib-dmi-hydrobase-java`|Java|API for Colorado's HydroBase database and web services|
|[`cdss-lib-dmi-nwsrfs-java`](https://github.com/OpenWaterFoundation/cdss-lib-dmi-nwsrfs-java)|`cdss-lib-dmi-nwsrfs-java`|Java|Legacy API for National Weather Service River Forecast Center models|
|[`cdss-lib-dmi-riversidedb-java`](https://github.com/OpenWaterFoundation/cdss-lib-dmi-riversidedb-java)|`cdss-lib-dmi-riversidedb-java`|Java|API for Riverside Technology Database|
|[`cdss-lib-dmi-satmonsys-java`](https://github.com/OpenWaterFoundation/cdss-lib-dmi-satmonsys-java)|`cdss-lib-dmi-satmonsys-java`|Java|API for Colorado's Satellite Monitoring System|
|[`cdss-lib-models-java`](https://github.com/OpenWaterFoundation/cdss-lib-models-java)|`cdss-lib-models-java`|Java|API for CDSS StateCU and StateMod models|
|[`cdss-lib-processor-ts-java`](https://github.com/OpenWaterFoundation/cdss-lib-processor-ts-java)|`cdss-lib-processor-ts-java`|Java|API for TSTool command processor and commands|
|[`cdss-util-buildtools`](https://github.com/OpenWaterFoundation/cdss-util-buildtools)|`cdss-util-buildtools`|NSIS, Launch4J, various|Utility programs to build TSTool installer|

The [New Developer](../dev-new/overview) documentation describes the typical way to set up the development environment.
In short, the above repositories are typically cloned from GitHub to a parent folder such as
`C:\Users\user\cdss-dev\TSTool\git-repos` on Windows.
Then the projects are imported into an Eclipse workspace.
The core TSTool software relies on the multiple Java code repositories to resolve dependencies.
Documentation and functional test repositories can be worked on independently of the code,
which allows contributions from non-programmers.

Code is for the most part split into commands and data persistence, which can be implemented as a datastore
(file, database, web service) or file I/O library.
If the API code is minimal, then such code often lives with the read and write commands in a Java package.
If the API code is substantial, it may be managed as a separate repository and corresponding project,
for example the State of Colorado's HydroBase library.

## Command File and Command Syntax ##

Need to describe the software design for command file and commands.

See also the [Command Syntax user documentation](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/command-syntax/).

## Java Runtime Environment  ##

TSTool is written in the Java language.
Java source code consists of files with `*.java` filename extension.
Code files include classes,  interfaces, enumerations, etc.
The source code is compiled into bytecode in class files with `*.class` filename extension.
These files are directly used in the development environment to run TSTool and are
packaged into Java Archive (`*.jar`) files for distribution and use at run-time.

A [Java Runtime Environment (JRE)](../resources#java) that is the same or newer than the Java version used in the development environment
is required to run TSTool in the operational environment.
Although it is possible to rely on a Java version on the computer, TSTool software
is distributed with its own JRE.  See the `jre_version` folder under the TSTool installation.
The JRE is then used to run TSTool via a TSTool launcher program.
On Windows, the open source [Launch4J](../resources#launch4j)
software is used to run TSTool and on Linux a `tstool` script is used.

## Command Processor ##

The command processor is the core class that handles processing commands shown in the TSTool UI and
when processing command files in batch mode.
The processor maintains lists of objects such as time series, tables, and datastores.
Properties are also maintained to control processing,
and include built-in properties such as input and output period,
and user defined properties that can be accessed using `${Property}` notation.

For historical reasons, there are two main classes,
which may be combined into a single class in the future:

* [TSEngine](https://github.com/OpenWaterFoundation/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSEngine.java) - original processor class
* [TSCommandProcessor](https://github.com/OpenWaterFoundation/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandProcessor.java) - modern command processor, calls TSEngine

## Command Factory ##

An instance of the [TSCommandFactory class](https://github.com/OpenWaterFoundation/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandFactory.java)
is used to parse commands as text and return an appropriate instance of a command class.
This class recognizes built-in commands and plugin commands.

## Command Interface and AbstractCommand Class ##

Specific command classes build on the [Command interface](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/Command.java),
which is implemented by the [AbstractCommand class](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/AbstractCommand.java).

Most commands extend `AbstractCommand`.

## Plugin Commands ##

Plugin commands are a feature that is under development.
The purpose of plugin commands is to let TSTool run third-part commands that are loaded from Jar files at runtime,
rather than being distributed with the core software.
More information will be added here later.

## CommandStatus Class ##

Every command includes an instance of the
[CommandStatus class](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/CommandStatus.java),
which maintains a log of messages generated by that command.
This allows fine-grained feedback on commands and flexibility
to generate reports after command workflows have run,
as opposed to filtering and sorting log files.

## Utility Packages ##

Many utility packages are used to provide general functionality.
See the [cdss-lib-common-java](https://github.com/OpenWaterFoundation/cdss-lib-common-java) package.

Over time, it may be possible to phase out some of this code given that the Java standard
libraries now provide similar functionality in some cases,
and third-party libraries are available.
However, using third-party libraries also increases the necessity to monitor, test, and respond
to changes in those packages.

## Logging ##

TSTool uses a "home grown" logging approach that was developed early in the TSTool development history
because other options were not available that could meet requirements.
See the [Message class](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Message/Message.java).
TSTool provides features to create a log file, view the log file contents interactively,
and control the amount of output to the log file.
Logging at a command level is also integrated via the `CommandStatus` as discussed above.

The current logging approach may be replaced with a standard logging library such as [SLF4J](../resources#slf4j)
if resources allow.

## Time Series Package ##

TSTool relies heavily on the [TS package](https://github.com/OpenWaterFoundation/cdss-lib-common-java/tree/master/src/RTi/TS)
for time series processing.
Significant effort has gone into designing the classes in this package to handle regular and irregular interval time series
in an efficient way.

## Datastores ##

Datastores have been introduced in TSTool in recent years to generally handle persistent data sources.
Datastores have primarily been applied to databases accessed via ODBC/JDBC and SOAP and REST web services.

A prototype design for plugin datastores is under development to facilitate integrating third-party
data sources with TSTool without having to change core code.

See the [datastore package](https://github.com/OpenWaterFoundation/cdss-lib-common-java/tree/master/src/riverside/datastore).

## Main TSTool Application ##

The main TSTool application class is launched in typical Java way via the
static [TSToolMain class](https://github.com/OpenWaterFoundation/cdss-app-tstool-main/blob/master/src/DWR/DMI/tstool/TSToolMain.java).
Command line parameters are parsed and TSTool is run in a mode that is requested.
For example, if running in batch mode, a
[TSCommandFileRunner class](https://github.com/OpenWaterFoundation/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandFileRunner.java)
is instantiated and the command file is run.
If running the GUI, then an instance of
[TSToolJFrame](https://github.com/OpenWaterFoundation/cdss-app-tstool-main/blob/master/src/DWR/DMI/tstool/TSTool_JFrame.java)
is created and the command file is run.

The GUI class is quite large and could benefit from refactoring.
However, much of the length results from the large number of menus and associated actions that
occur in responding to those menus.
Components could be refactored to act autonomous of the TSTool Main UI, but this would require evaluation.

## Built-in Test Framework ##

One of the major features of TSTool is a built-in test framework that facilitates testing commands in the full application.

* [cdss-app-tstool-test test repository](https://github.com/OpenWaterFoundation/cdss-app-tstool-test)
* [Quality Control chapter of user documentation](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/quality-control/quality-control/)

## Future Design Elements ##

Major enhancements that are envisioned are listed below, in no particular order.
This list is not comprehensive and additional items will be added as
legacy documentation is migrated to this developer manual and repository issues tracker.
Some enhancements will require significant effort because features are used throughout the software.

1. Upgrade to use Java 9.
	* Utilize new features.
	* Evaluate the module system to help with dependency management and plugins.
2. Update the development environment to support 32-bit and 64-bit runtimes
	* Focus is currently 32-bit because some components such as HEC-RAS API uses
	32-bit native libraries.
3. Enable robust plugin support to facilitate third-party component development.
4. Move to online documentation and phase out Word/PDF packaging in installer.
5. Update installer to use latest NSIS and Launch4J.
6. Update development environment to use Maven for dependency management and automation.
7. Update development environment to NOT store Eclipse artifacts in repositories,
to support more development environments.
8. Split currently embedded packages into plugins for components that are maintained
by third parties (rather than core CDSS/TSTool team), potentially:
	* ReclamationHDB datastore
	* RiversideDB datastore
	* National Weather Service datastores
9. Migrate logging to SL4J logging framework.
10. Evaluate integration with Python/Jython and other languages.
11. General code cleanup of legacy code.
12. Add support for indentation in command files.
13. Evaluate migrating from Swing to JavaFX user interface framework.
