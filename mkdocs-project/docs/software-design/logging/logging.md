# Logging #

* [Introduction](#introduction)
* [Log Messages](#log-messages)
* [Log Files](#log-files)
* [Setting Logging Levels](#setting-logging-levels)
* [Log File Viewer](#log-file-viewer)
* [Potential Future Changes](#potential-future-changes)

-------------

## Introduction ##

TSTool uses a "home grown" logging approach that was developed early in the TSTool development history
because other options were not available that could meet requirements.
See the [Message package](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Message/)
and in particular the
[Message class](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Message/Message.java) class.
TSTool provides features to create a log file, view the log file contents interactively,
and control the amount of output to the log file.
Logging at a command level is also integrated via the `CommandStatus` as discussed above.

## Log Messages ##

Useful information can be logged for status, debug, warning, and failure messages.
Logging messages can further be controlled to output to console (standard output to terminal window),
log file, and user interface (any component that listens to messages).
The general approach is to minimize logging in order to improve performance,
but use logging to provide progress information and inform on issues.

Numeric logging levels can be set for each message type.
Whereas logging frameworks typically set this in a "handler" feature,
the TSTool logging uses configuration data and levels passed in logging methods.

The following is an example of a typical warning message in library code.
Note that the method name (called `routine`) is constructed based on class
information rather stack track, which might be used by a logging framework.

```
String routine = getClass().getName() + ".checkCommandParameters";
message = "Error requesting WorkingDir from processor.";
Message.printWarning(3, routine, message );
```

Debug messages are typically wrapped in a check to determine if debug level is active (non-zero).
This improves performance because formatting can be avoid if not in debug mode.

```
resultString = IOUtil.readFromURL(urlString.toString() );
if ( Message.isDebugOn ) {
    Message.printDebug(1,routine,"Returned data="+resultString);
}
```
Logging messages in commands are further "decorated" with command number to help the log file viewer
associate log messages with commands.  The `formatMessageTag` method uses the `command_tag`
(generally the command number 1+ in the command file).

```
message = "Error requesting DateTime(DateTime=" + InputStart + ") from processor.";
Message.printWarning(warning_level,
    MessageUtil.formatMessageTag( command_tag, ++warning_count), routine, message );
```

## Log Files ##

TSTool opens a default log file at startup.
Whereas older versions opened the log file in the software installation folder,
newer versions use a startup log file in the `.tstool/log/` folder in the users files, whether Windows or Linux.
This ensures that a log file can be written without administrator permissions.

It is generally recommended that workflows use the
[`StartLog`](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/StartLog/StartLog/)
command to open a log file that has the same name as the command file, appended with `.log`.
The log file specific to the command file can then be used to troubleshoot the command file.
This approach is used with automated testing to ensure that an artifact exists to review the run.
Log files are typically omitted from repositories using the `.gitignore` file.

Opening a log file with the
[`StartLog`](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/StartLog/StartLog/) command
closes the previous log file and starts the new log file.
Consequently, use the startup log file to troubleshoot startup issues.

## Setting Logging Levels ##

Logging levels are set in a number of ways:

1. Logging levels are set in the
[Message class](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Message/Message.java) class.
2. The [TSTool_Main](https://github.com/OpenWaterFoundation/cdss-app-tstool-main/blob/master/src/DWR/DMI/tstool/TSToolMain.java)
class adjusts based on TSTool defaults and optionally command line parameters.
3. User can interactively change levels via the ***Tools / Diagnostics...*** menu.
4. The [`SetDebugLevel`](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/SetDebugLevel/SetDebugLevel/) and
[`SetWarningLevel`](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/SetWarningLevel/SetWarningLevel/) commands can change logging levels,
and are typically used with [`StartLog`](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/StartLog/StartLog/) command.

Log levels are typically left at the default unless troubleshooting the application.
In this case, 

## Log File Viewer ##

TSTool's ***Tools / View Log File*** menu displays an interactive log file viewer.
This tool uses custom logging features, such as using the command line number in a command file to
cross-reference log messages.

## Potential Future Changes ##

The current logging approach may be replaced with a standard logging library such as [SLF4J](../resources#slf4j)
if resources allow.
Significant redesign may be necessary in order to continue providing features consistent with the existing software,
such as the log file viewer.
On the other hand, redesigning the logging system will likely provide better integration with component libraries
that use a standard framework.

One issue that needs to be addressed is that the
[Message class](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Message/Message.java) class
is an singleton that is shared across an application.
This limits the ability to create "pooled" applications or split logging.
This has not been an issue yet.
