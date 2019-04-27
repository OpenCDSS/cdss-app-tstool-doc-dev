# TSTool Application #

* [Introduction](#introduction)
* [Launching](#launching)
* [Configuration](#configuration)
* [User Interface (UI)](#user-interface-ui)

-----

## Introduction ##

The TSTool main application is the entry point into the software and is used for multiple run modes.
Command parameters are parsed to determine how to launch the application and then
appropriate classes are instantiated.

TSTool configuration can be complex due to the number of data sources that are supported.
As much as possible, the configuration is distributed with useful defaults,
and configuration files are simple text files that can be modified as appropriate.

## Launching ##

The TSTool main application class is launched in typical Java way via the
static [TSToolMain class](https://github.com/OpenCDSS/cdss-app-tstool-main/blob/master/src/DWR/DMI/tstool/TSToolMain.java).
Command line parameters are parsed and TSTool is run in a mode that is requested.

For example, if running in batch mode, a
[TSCommandFileRunner class](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandFileRunner.java)
is instantiated and the command file is run.

If running the GUI, then an instance of
[TSToolJFrame](https://github.com/OpenCDSS/cdss-app-tstool-main/blob/master/src/DWR/DMI/tstool/TSTool_JFrame.java)
is created and the command file is run.

On Windows, the [Launch4J](../../resources.md#launch4j) software is used to create an
executable program to launch TSTool.
This allows the `tstool.exe` program to be run.
Launch4j provides numerous features to optimize Java program start-up on Windows.

See also:

* [Running TSTool in Various Modes appendix of User Documentation](http://opencdss.state.co.us/tstool/latest/doc-user/appendix-running/running/)

## Configuration ##

TSTool is configured via a number of simple text files.
Simple `Property=Value` syntax has been used and
[INI format](https://en.wikipedia.org/wiki/INI_file)
with sections and #-comments is used for `TSTool.cfg`.
These simple formats will likely continue to be used, although JSON may be adopted where it has benefits,
such as hierarchical time series product files.

The [Installation TSTool appendix in the User Documentation](http://opencdss.state.co.us/tstool/latest/doc-user/appendix-install/install/),
as well as [Datastore documentation](http://opencdss.state.co.us/tstool/latest/doc-user/datastore-ref/overview/)
describes configuration files.

## User Interface (UI) ##

The
[TSToolJFrame](https://github.com/OpenCDSS/cdss-app-tstool-main/blob/master/src/DWR/DMI/tstool/TSTool_JFrame.java)
class is quite large and could benefit from refactoring.
However, much of the length results from the large number of menus and associated actions that
occur in responding to those menus.
Components could be refactored to act autonomous of the TSTool Main UI, but this would require evaluation.

See the [User Interface Software Design documentation](../ui/ui.md).

