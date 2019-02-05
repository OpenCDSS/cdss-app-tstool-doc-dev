# Plugin Datastores #

A prototype design for plugin datastores is under development to facilitate integrating third-party
data sources with TSTool without having to change core code.

See the [datastore package](https://github.com/OpenCDSS/cdss-lib-common-java/tree/master/src/riverside/datastore)
and [PluginDataStore](https://github.com/OpenCDSS/cdss-lib-common-java/blob/master/src/riverside/datastore/PluginDataStore.java) interface.

Plugin commands are a also a new feature that is under development.
The purpose of plugin commands is to let TSTool run third-part commands that are loaded from Jar files at runtime,
rather than being distributed with the core software.
Plugin commands are often made available with datastores to read and write datastore data.
See also [Plugin Commands](../plugin-commands/plugin-commands.md).
