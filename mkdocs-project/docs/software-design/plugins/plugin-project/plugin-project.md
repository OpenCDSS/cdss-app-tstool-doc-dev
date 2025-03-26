# TSTool / Software Design / Plugins / Plugin Project #

*   [Introduction](#introduction)
*   [Add a New Plugin Project to Eclipse](#add-a-new-plugin-project-to-eclipse)
    +   [Create a Git Repository](#create-a-git-repository)
    +   [Add a New Maven Project](#add-a-new-maven-project)
    +   [Configure the Eclipse Project](#configure-the-eclipse-project)
    +   [Configure the POM](#configure-the-pom)
*   [Next Steps](#next-steps)

----------------------

## Introduction ##

This documentation explains how to initialize a new Eclipse project for a TSTool plugin.
The examples shown use Java 8, Eclipse 2019-03, and TSTool 14.x.
Different software versions should have similar configuration steps but will vary.

A plugin in the development environment is enabled by adding a project to the main TSTool Eclipse workspace,
which uses a separate Git repository.
The core TSTool product can be developed stand-alone, or one or more plugins can be developed with the core product.

Although the plugin's code is edited with the TSTool application code in Eclipse,
it must be run by deploying the plugin to the user's run-time TSTool files so that TSTool can load it dynamically as in production.
A script is used to compile and create the `jar` file in the user's TSTool files.
Then, when TSTool is run from Eclipse, it detects the plugin as if in production.
This approach also forces the developer to test the plugin as if a user during development.

The remainder of this documentation describes how to add a new plugin project to the Eclipse workspace.

## Add a New Plugin Project to Eclipse ##

The following example illustrates how to add a new plugin project to Eclipse,
in this case a plugin that integrates with Amazon Web Services.
Java 8 and Maven project is used.

A convention used by the Open Water Foundation is to include a `doc-init` folder in the repository with
notes explaining how to initialize the repository.
Then, adding new repositories can follow similar instructions.

### Create a Git Repository ###

It is recommended to create an empty plugin repository in GitHub or another cloud repository
first and then add files in Eclipse, committing as usual to save incremental work.
This approach has been tested with GitHub and Bitbucket, and GitHub is used as an example below.

1.  Create a GitHub repository that will be used for the plugin, in this example `owf-tstool-aws-plugin`.
    The repository can be empty.
2.  Clone the repository under the `git-repos` folder that is recommended for TSTool development (this should have been set up previously).
    For example, for Windows use a folder like
    `C:\Users\user\cdss-dev\TSTool\git-repos\owf-tstool-aws-plugin`.
3.  Add normal files such as `.gitignre`, `.gitattributes`, and `README.md`.
    If another plugin is available, it is often easy to copy files and modify as needed.

### Add a New Maven Project ###

Maven should be used for newer projects because it manages software dependencies.
A Maven Project Object Model (POM file) `*.pom` is used to list software dependencies and other configuration information.
Required `jar` files are automatically downloaded and are maintained in a local file repository for the user.

In this approach, the Git repository does not contain copies of jar files needed for the project.
However, the plugin installer that is deployed for the production system contains all necessary `jar` files.
Consequently, if the public Maven repository containing an old dependency `jar` file
is removed in the future, the file can be retrieved from the plugin installation file.
However, it is likely that older software will not need to be installed and recent Maven files should be sufficient.

Add a new project using ***File / New / Other / Maven / Maven Project***, which shows the following:

**<p style="text-align: center;">
![Add a new Maven project: select Maven project](images/new-project-1.png)
</p>**

**<p style="text-align: center;">
Add a New Maven Project - Select Maven Project (<a href="../images/new-project-1.png">see full-size image</a>)
</p>**

Press ***Next >*** to continue.  The following will be shown.

**<p style="text-align: center;">
![Add a New Maven Project](images/new-project-2a.png)
</p>**

**<p style="text-align: center;">
Add a New Maven Project - New Maven Project (<a href="../images/new-project-2a.png">see full-size image</a>)
</p>**

Unselect the ***Use default Workspace location*** choice
because the project files will exist in the Git repository working files.
Use the ***Browse...*** button to select the Git repository folder, which will result in settings similar to the following.

**<p style="text-align: center;">
![Add a New Maven Project: select folder](images/new-project-2b.png)
</p>**

**<p style="text-align: center;">
Add a New Maven Project - New Maven Project (<a href="../images/new-project-2b.png">see full-size image</a>)
</p>**

Press ***Next >*** to continue.

Select the Maven project archetype as shown in the following dialog.
The wizard will create the folders used in the project, which follow Maven "archetype" conventions.
See the [Maven Archetypes](https://maven.apache.org/archetypes/) documentation.

The archetype does not appear to be stored in the Eclipse files after the fact.
In this case select the `maven-archtype-quickstart` based on experience with other plugins,
which involves simple Java files (not J2EE, etc.).

**<p style="text-align: center;">
![Specify the Maven project archetype](images/new-project-3-archetype.png)
</p>**

**<p style="text-align: center;">
Add a New Maven Project - Maven Archetype (<a href="../images/new-project-3-archetype.png">see full-size image</a>)
</p>**

Press ***Next >*** to continue.

Specify the Archetype parameters, which will be inserted at the top of the `*.pom` file and are used in the Maven dependency checks:

*   ***Group Id*** - it is typical to use the organization domain in reverse order,
    or a Java package hierarchy (with folder slashes equivalent to periods)
*   ***Artifact Id*** - use the name of the repository, which should be a distinct name that follows appropriate conventions
*   ***Version*** - default is OK, can be changed over time if the plugin is distributed as a Maven package
*   ***Package*** - the Java package that will be created in the source code (`src`) folder,
    can use reverse domain name conventions or other suitable package name
    (in this example a verbose hierarchical package name is used)

Because the plugin code is packaged as a run-time addition to TSTool,
it is not generally distributed as a Maven package.
Consequently, the setup procedure is mainly to used to configure the Eclipse files.

**<p style="text-align: center;">
![Maven archetype parameters](images/new-project-4-archetype-parameters.png)
</p>**

**<p style="text-align: center;">
Add a New Maven Project - Maven Archetype Parameters (<a href="../images/new-project-4-archetype-parameters.png">see full-size image</a>)
</p>**

Press ***Finish*** to finish.  The following package folders and resources will be initialized (or similar).

**<p style="text-align: center;">
![Initial Eclipse resources for new Maven project](images/new-project-5-eclipse-new.png)
</p>**

**<p style="text-align: center;">
Add a New Maven Project - Initial Eclipse Resources (<a href="../images/new-project-5-eclipse-new.png">see full-size image</a>)
</p>**

The Git working files will contain a folder matching the Maven artifact name,
which in this case will result in the parent Git repository folder and the child Maven folder using the same name
(`owf-tstool-aws-plugin/owf-tstool-aws-plugin`).
The Git repository working files will contain a folder for the package.
However, no files will be present in the `owf-tstool-aws-plugin/src/main/java/org/openwaterfoundation/tstool/plugin/aws` folder (or similar).

The initial files can be saved to Git, although empty folders will not result in a commit.
The hidden file `.project` and hidden folder `.settings` can be committed,
although it may be necessary to gitignore settings files in the future if they conflict between developers.

### Configure the Eclipse Project ###

The initial Eclipse project will not have knowledge about other workspace projects or settings that are needed
for development in the TSTool framework.
The plugin will typically relay on at least two libraries that are part of TSTool,
and potentially other third-party libraries (e.g, Jackson for reading and writing JSON and CSV files).

Right-click on the project in ***Package Explorer*** view and open ***Properties***.

Change the ***Java Build Path / Projects*** tab settings to add the following projects that are needed for plugin development.

**<p style="text-align: center;">
![Eclipse Java build path](images/new-project-6-eclipse-properties.png)
</p>**

**<p style="text-align: center;">
Project Properties - Eclipse Java Build Path (<a href="../images/new-project-6-eclipse-properties.png">see full-size image</a>)
</p>**

Change the ***Java Compiler*** tab settings to use JDK 11 compliance
(or whichever Java version is being used for TSTool development)
and workspace settings (double click on ***Java Compiler***).
The ***JDK Compliance*** must be configured before un-checking the ***Enable project specific settings***.
This generally simplifies the configuration to use the workspace settings across all projects.

Although it is possible to distribute a plugin that uses an earlier Java version than the TSTool Java version,
it is recommended that the same version is used.
The TSTool Java version is updated relatively infrequently to minimize disruptions for developers.

**<p style="text-align: center;">
![Java compiler properties](images/new-project-7-eclipse-properties-compiler.png)
</p>**

**<p style="text-align: center;">
Project Properties - Java Compiler (<a href="../images/new-project-7-eclipse-properties-compiler.png">see full-size image</a>)
</p>**

## Configure the POM ##

The `pom.xml` file for the project must be configured for the plugin.
For simple plugins this typically requires adding to the `<dependencies>` for third-party software packages.
Note that configuration discussed above will allow using other TSTool code without adding to the Maven dependencies.
TSTool projects may explicitly include `jar` files that can be used by the plugin,
rather than adding a potentially conflicting dependency in the `pom.xml` file.

For example, the Amazon Web Services API documentation indicates the necessary POM dependencies.
After updating the `pom.xml` file, right-click on the project and use ***Maven / Update Project...***.

Additional documentation needs to be added to explain how to package the dependencies in the plugin,
especially when packages are already used in TSTool.
For example, Maven uses the Jackson and Apache commons logging software, which is also used by TSTool elsewhere.
It is possible to include additional jar files in the deployed `plugins` folder but this needs to be tested.
One option is to ensure that the overlapping plugin dependency versions are the same in TSTool as the plugin
so that the software that is found will work in any case.

**<p style="text-align: center;">
![Maven dependencies](images/new-project-8-eclipse-maven-dependencies.png)
</p>**

**<p style="text-align: center;">
Project Properties - Maven Dependencies (<a href="../images/new-project-8-eclipse-maven-dependencies.png">see full-size image</a>)
</p>**

## Next Steps ##

Once the project is configured, code can be added for the plugin.

See the documentation for adding a datastore and command:

*   [Plugin Datastores](../plugin-datastores/plugin-datastores.md) - information about adding a plugin for a datastore
*   [Plugin Commands](../plugin-commands/plugin-commands.md) - information about adding a plugin for a command

See the documentation for building the plugin so that it can be used in the development environment:

*   [Plugin Packaging and Installation](../overview.md#plugin-packaging-and-installation) documentation for more information
