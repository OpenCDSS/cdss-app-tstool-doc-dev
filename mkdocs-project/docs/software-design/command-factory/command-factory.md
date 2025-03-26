# TSTool / Software Design / Command Factory #

An instance of the [TSCommandFactory class](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandFactory.java)
is used to parse commands as text and return an appropriate instance of a command class.
This class recognizes built-in commands and plugin commands.
Currently the command factory imports all known commands.
An alternative approach could be implemented similar to plugins whereby
command classes do not need to be imported at compile time;
however, this approach has not been needed to date.

The factory is called by the [TSTool UI](../ui/ui.md) when adding new commands or editing commands.

It is also called when reading in a command file to run in batch mode,
for example via [`TSCommandFileRunner`](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandFileRunner.java).
