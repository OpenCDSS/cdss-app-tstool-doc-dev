# TSTool / Software Development / Plugins #

*   [Introduction](#introduction)
*   [Plugin Eclipse Project](#plugin-eclipse-project)
*   [Plugin Command](#plugin-command)
*   [Plugin Datastore](#plugin-datastore)
*   [Plugin Tests](#plugin-tests)
*   [Plugin Documentation](#plugin-documentation)
*   [Plugin Packaging and Installation](#plugin-packaging-and-installation)
    +   [`PluginMeta.java` Class](#pluginmetajava-class)
    +   [`MANIFEST.MF` Resource File](#manifestmf-resource-file)
    +   [Build Script](#build-script)

----------------------

## Introduction ##

This documentation explains how to implement TSTool plugins.
Plugins were introduced in TSTool 12, were significantly expanded in TSTool 14+,
and the design was further formalized in TSTool 15,
including adding the plugin manager.

The examples shown use Java 8 (or later), Eclipse 2019-03 (or later), and TSTool 14.x (or later).
Different software versions should have similar configuration steps but will vary.

TSTool plugins provide add-on features that are not provided by the core TSTool software.
Plugins are typically implemented for the following:

1.   Datastore, for example to integrate TSTool with a web service, database,
     or a modeling environment.
2.   Commands:
    1.   Read and/or write commands for a plugin datastore.
    2.   Provide some other functionality specific to a technology or set of third-part tools
         (e.g., integration with Amazon Web Services API).

A plugin can include zero or one datastores, and zero or more commands.

There can be conflicts in a plugin's dependency versions.
This is an area where additional development may need to occur.

Plugins in the development environment are developed by adding a project to the main TSTool Eclipse workspace,
but the plugin **is not** added to the built-in TSTool build system.
Instead, a script is used to compile and create the `jar` file in the user's TSTool files.
Then, when TSTool is run from Eclipse, it detects the plugin as if in production.
This approach also forces the developer to test the plugin as if a user during development.
Deploying the plugin involves packaging the files from a developer's user files.

## Plugin Eclipse Project ##

Plugins are typically developed using a separate Git repository and are added as a separate Eclipse project.

See the [Plugin Project](plugin-project/plugin-project.md) documentation.

## Plugin Command ##

A plugin can contain one or more commands,
which will automatically be loaded by TSTool and will be available in the ***Commands(Plugin)*** menu.

See the [Plugin Commands](plugin-commands/plugin-commands.md) documentation.

## Plugin Datastore ##

A plugin can contain code to integrate with a datastore,
for example a local database, web service API, or model files.
A plugin that contains datastore integration typically also contains at least one command to read the datastore's contents.

A datastore plugin can be used to configure multiple datastores.

See the [Plugin Datastores](plugin-datastores/plugin-datastores.md) documentation.

## Plugin Packaging and Installation ##

A plugin is packaged into a zip file that can be installed in a user's TSTool files.
For example, see TSTool plugins available from the [Open Water Foundation](https://software.openwaterfoundation.org).

The following illustrates the typical plugin installation folder structure.
The version folder (e.g., `2.0.0`) is understood by TSTool 15+ and is being phased in
to allow multiple versions of plugins to be installed at the same time.
TSTool versions older than 15 cannot properly handle this convention and will load multiple versions of a plugin if found
(fix by moving or removing plugin versions so that only one version is found).
As of 2021-03-24, all plugins are being updated to use the version folder consistent with TSTool 15+
and TSTool will only load the most recent (or otherwise best compatible)
version of a plugin.

```
C:\Users\user\.tstool\15\plugins\      Windows
/home/user/.tstool/15/plugins/         Linux (Linux folder separates are used below)
  owf-tstool-aws-plugin/
    1.5.7/
      owf-tstool-aws-plugin-1.5.7.jar
      dep/
    2.0.0/
      owf-tstool-aws-plugin-2.0.0.jar
      dep/
  owf-tstool-bitbucket-plugin/
  owf-tstool-googledrive-plugin/
  owf-tstool-kiwis-plugin/
  owf-tstool-timesheetscom-plugin/
  owf-tstool-usweathergov-plugin/
  owf-tstool-zabbix-plugin/
  trilynx-tstool-nsdataws-plugin/
```

The optional `dep/` folder in the above contains dependency `jar` files needed by the plugin.
These typically correspond to the Maven dependencies indicated by the `pom` file when
setting up the plugin project in Eclipse (see the [Plugin Project](plugin-project/plugin-project.md) documentation).

A plugin in the deployed environment is packaged as a Java `jar` file that is
installed in the software installation `plugins` folder
or a user's `.tstool/##/plugins` folder.
TSTool will automatically recognize a properly constructed plugin and will enable the plugin
datastores and commands.

The plugin jar file's `resources/META-INF/MANIFEST.MF` file and plugin interface methods are used to provide information
about the plugin so that TSTool can display datastore and command features in the user interface.
The following sections describe plugin configuration data that impact the installer and run-time TSTool behavior.

### `PluginMeta.java` Class ##

The `PluginMeta.java` class described in the [Plugin Commands](plugin-commands/plugin-commands.md) documentation typically includes
the plugin version for use at runtime, which is easily accessible by Java code.
This version can also be used when building the plugin installer, as described below.

### `MANIFEST.MF` Resource File ###

The `resources/META-INF/MANIFEST.MF` file should be created in the Eclipse project,
with information similar to the following example.
This information can be used when building the plugin installer and at run-time by TSTool's plugin manager.

```
Comment01: Manifest file to distribute with the
Comment02: TimesheetsComDataStore.jar file.
Comment03: Maximum line length is 72 characters to avoid truncation.
Comment04: Indent continued lines by a single space.
Comment05: DataStore-Class is the path to the datastore class.
Comment06: DataStoreFactory-Class is the path to the datastore factory class.
Comment07: Command-Class1 is the path to a command class.
Comment08: Increment the number as needed for the number of command classes.
Comment09: Class-Path contains the dep/ folder for dependency jar files.
manifest-Version: 1.0
Plugin-Name: trilynx-tstool-timesheetscom-plugin
Plugin-Version: 2.0.0
TSTool-Version: >= 15.0.0
DataStore-Class: org.openwaterfoundation.tstool.plugin.timesheetscom.datastore.
 TimesheetsComDataStore
DataStoreFactory-Class: org.openwaterfoundation.tstool.plugin.timesheetscom.
 datastore.TimesheetsComDataStoreFactory
Command-Class1: org.openwaterfoundation.tstool.plugin.timesheetscom.
 commands.ReadTimesheetsCom_Command
Class-Path: dep/
```

**<p style="text-align: center;">
Example `MANIFEST.MF` File for a Plugin with Datastore and Command
</p>**

If necessary, an older software installer (such as for an older version of Java) can be rereleased as a newer maintenance version
with updated `MANIFEST.MF` file, for example using the `TSTool-Version` attribute
to indicate which TSTool version is required as changes are made.
Newer versions of TSTool may be required to use such information at run-time.
Plugin manager features are expected to stablize in version 15+ releases.

Each line in the `MANIFEST.MF` file can only be 72 characters long (extra characters are ignored).
Lines that inlcude a space at the beginning are appended to the previous line.
The attributes in the manifest file are as follows.

**<p style="text-align: center;">
`MANIFEST.MF` Attributes (in order of the above example)
</p>**

| **Attribute**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | **Description** |
| -- | -- |
| `CommentNN` | Comment line.  The sequential number `NN` ensures that when read as an attribute the values are unique. |
| `manifest-version` | The Java Jar file manifest version, OK to keep the default value. |
| `Plugin-Name` | The TSTool plugin name (e.g., `owf-tstool-aws-plugin`), which should match the project folder and installation file. |
| `Plugin-Version` | The TSTool plugin version (e.g., `1.2.3`), which should match the version in the `PluginMeta.java` file, the installation version folder, and the end of the plugin `jar` file. |
| `TSTool-Version` | An expression that indicates the TSTool version for compatibility, to ensure Java version compatibility or TSTool integration compatibility.  For example `>= 15.0.0` indicates that the TSTool version must be at least version `15.0.0`. If not specified, TSTool will use the installation folder if found at runtime or the end of the plugin folder. |
| `DataStore-ClassN` | The package for a plugin datastore.  TSTool will load this class to be able to load datastores with matching configuration files. |
| `DataStoreFactory-ClassN` | The package for a plugin datastore factory class.  TSTool will load this class to be able to load the datastore configuration file. |
| `Command-ClassN` | The package for a plugin command.  TSTool will load this class and enable a corresponding ***Commands(Plugin)*** menu. A sequential number starting at `1` should be used to uniquely identify each command. |
| `Class-Path` | The folder where plugin dependency `jar` files are stored, typically `dep/`, which is a folder in the same location as the plugin `jar` file.  The folder will be added to the Java class path.  The folder can be empty. |

## Plugin Tests ##

Plugin automated tests can be implemented similar to tests for TSTool's built-in features.
It is recommended to create a folder structure similar to the following in the plugin's repository files:

```
test/                                      Top-level test folder.
  README.md                                Documentation to explain how to create and run tests.
  commands/                                Tests for each command.
     CommandName/                          Folder for a command's automated tests.
       test-CommandName-modifier.tstool    Typical test command file name.
       expected-results/                   Expected results from a test.
       results/                            Results from a test.
         .gitignore                        Ignore all files except .gitignore.
  test-suite/                              Folder to create and run test suites.
    create/                                Script to san for tests and create a run suite.
    run/                                   Location to create suite for running.
      results/                             Dynamic output.
        .gitignore                         Ignore all files except .gitignore.
```

Because tests may depend on specific datastores for an organization,
and even private datastores, tests may only run in specific configurations.

## Plugin Documentation ##

Plugin documentation can be created similar to TSTool's main documentation,
for example using the MkDocs software, which creates a static website from markdown files.
For example, create a `doc-user-mkdocs-project` in the repository's main folder,
similar to the following:

```
doc-user-mkdocs-project/         Documentation for user documentation.
  build-util/                    Scripts to view documentation during editing,
                                 and deploy the static website for viewing.
  docs/                          Source documents.
  mkdocs.yml                     MkDocs configuration file.
  README.md                      Documentation to explain how to create and deploy the documentation.
  resources/                     Additional resources as input to documentation
                                 (e.g., PowerPoints to create diagrams, etc.).
  site/                          Dynamic content created when building the documentation.
```

The repository's main `.gitignore` file can be used to ignore the dynamic `site` files.

## Build Script ##

The plugin code must be compiled and packaged ito an istaller that can be installed for production use.
A multi-step process is recommended, as follows, using the `trilynx-tstool-aws-plugin` as an example
(see the Open Water Foundation repository files:
[`https://github.com/OpenWaterFoundation/owf-tstool-aws-plugin/tree/main/build-util`](https://github.com/OpenWaterFoundation/owf-tstool-aws-plugin/tree/main/build-util)).
The scripts are typically located in a `build-util` (or similar) folder in the repository and are run with Git Bash or similar.
Note that plugins are typically **not** developed for the State of Colorado and are therefore
hosted by third parties like the Open Water Foundation.

1.  `0-create-plugin-jar.bash`:
    1.  Runs command-line `maven` software to compile and create the plugin's `jar` file
        and copy to the user's `.tstool` files so that running TSTool will find the plugin.
    2.  Runs command-line `maven` software to determine the plugin's dependency `jar` files
        (from the Maven repository) and copy to the `dep/` folder in the user's plugin files.
    3.  Note that it may be necessary to exit all TSTool sessions because if TSTool is running,
        it may lock plugin `jar` files from being overwritten.
2.  `1-create-installer.bash`:
    1.  Create the installer `zip` file from the first in the first step and save in a temporary file.
3.  `2-copy-to-owf-amazon-s3.bash`:
    1.  Copy the installer `zip` file to the cloud for public access,
        in this case to the Open Water Foundation's [https://software.openwaterfoundation.org](https://software.openwaterfoundation.org/tstool-aws-plugin) web page.
    2.  Optionally, call the next script.
4.  `3-create-s3-index.bash`:
    1.  Create the plugin landing page for downloads,
        which lists all uploaded installers for different versions.

The first step is typically run repeatedly during development to allow running the latest code changes during development and testing.
Steps 2-4 are only run when creating plugin software releases.
