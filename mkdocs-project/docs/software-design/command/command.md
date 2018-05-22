# Command #

* [Introduction](#introduction)
* [Command Interface](#command-interface) - basic behavior requirements
* [AbstractCommand Class](#abstractcommand-class) - default implementation of `CommandInterface`
* [Specific Command Class](#specific-command-class)
* [CommandStatusProvider Interface](#commandstatusprovider-interface) - for command log/status access
* [CommandDiscovable Interface](#commanddiscoverable-interface) - to run in discovery (pre-run) mode
* [FileGenerator Interface](#file-generator-interface) - for commands that create output files
* [CommandProcessorEventProvider Interface](#commandprocessoreventprovider-interface) - to allow processor to listen for command events

----

## Introduction ##

This documentation focuses on the design of command classes.

The [TSCommandProcessor](https://github.com/OpenWaterFoundation/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandProcessor.java)
manages a list of commands, which allows the commands to be interacted with in the UI and run in batch mode.
The processor performs tasks that are general but does not perform analysis.

Command instances are created using the [TSCommandFactory Class](../command-factory/command-factory) (see separate discussion).

Command classes implement the functionality to perform data manipulation, analysis, and product generation.
The command design provides flexibility and has been used to implement a wide variety of computational functionality.
Command classes are typically created by implementing interfaces:

* [Specific Command class](#specific-command-class)
	+ Extends [AbstractCommand](#abstractcommand-class) - manages command data and provides default implementation
		- `AbstractCommand` implements [Command Interface](#command-interface)
	+ Implements:
		- [CommandStatusProvider interface](#commandstatusprovider-interface) - methods to provide command log/status
		- [CommandDiscoverable interface](#commanddiscoverable-interface) - methods to run in discovery (pre-run) mode
		- [FileGenerator interface](#filegenerator-interface) - method to retrieve list of generated files

## Command Interface ##

Commands implement the
[Command interface](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/Command.java)
and must implement the methods from the interface.
These methods have been determined to be the minimal behavior needed to implement functioning commands in TSTool.
Specific commands typically extend the [AbstractCommand class](#abstractcommand-class), which provides default behavior.

## AbstractCommand Class ##

The [AbstractCommand class](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/AbstractCommand.java)
implements the
[Command interface](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/Command.java)
and provides default functionality for several methods such as `parseCommand()` and `toString()`.
This class can be enhanced to provide additional functionality to all commands.

## Specific Command Class ##

Commands should extend `AbstractCommand` and implement their own `runCommands()` and other command-specific functionality.
Command class names typically match the command name, for example `NewTimeSeries_Command`.
The verbose `_Command` is used to clearly indicate commands, given the larger number of classes used in TSTool.

## CommandStatusProvider Interface ##

The [CommandStatusProvider](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/CommandStatusProvider.java)
interface defines behavior needed by the TSTool UI to display command log messages and status.
Command status features allow messages relevant to a command to be accumulated on the command instance,
simplifying tracking of success and failure.  See also the [CommandStatus](../commandstatus/commandstatus) documentation section.

## CommandDiscoverable Interface ##

The [CommandDiscoverable](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/CommandDiscoverable.java)
interface is implemented by commands that can run in "discovery" mode.
For example, the [`NewTimeSeries`](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/NewTimeSeries/NewTimeSeries/)
command parameters provide enough information for the command
to indicate that a new time series will have a specific identifier and alias.
The discovery information is used to provide command editors for later commands with
information that can be displayed, such as a choice of time series.

The discovery mode is generally implemented for commands that create time series and tables, or set processor properties.
The command will run in partial mode by knowing that discovery has been requested.

If `${Property}` notation is used, then it will be difficult or impossible for commands to run in discovery mode
because the value of the property will not be known until run time,
especially if property values are set from from a sequence of commands.
However, it is often OK to pass through the property notation string as the discovery results.
For example, knowing that a time series with identifier `${SomeLoc}.${SomeSource}.${SomeType}.${SomeInterval}` is created
in a previous command is OK because the same TSID string could be used as dynamic input to a later command.

## FileGenerator Interface ##

The [FileGenerator](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/FileGenerator.java)
interface indicates that a command generates files and can provide the names of those files.

The TSTool UI provides ***Results / Output Files*** section to list output files from commands.
To list the files, the TSTool UI requests the lists of files from all commands.
Each command is able to provide filenames from its processing.
This ensures that there is no disconnect between command state and how a command's output is used.

## CommandProcessorEventProvider Interface ##

The [CommandProcessorEventProvider](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/IO/CommandProcessorEventProvider.java)
interface indicates that a processor can listen for events generated by the command.
This functionality is being evaluated as a general way to pass information from command to processor during execution.
