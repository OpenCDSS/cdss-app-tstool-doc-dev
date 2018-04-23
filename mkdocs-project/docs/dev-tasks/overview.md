# TSTool / Development Tasks / Overview #

Development tasks are the day-to-day work that a software developer does to enhance TSTool software
to add new functionality, fix bugs, etc.
This documentation describes common tasks, roughly in the order from design to deployment

* [Run Eclipse](#run-eclipse) - how to start Eclipse
* [Designing Software](#designing-software) - how to go about software design
* [Version Control with Git](#versioning) - how should developers do branch, merge, commit messages, tags, etc.
* [Documenting](#documenting) - how developers should document code, API, create developer and user documentation
* [Troubleshooting Eclipse](#troubleshooting-eclipse) - figuring out why Eclipse is not working, and responding to Eclipse errors (beyond code syntax errors)
* [Coding](#coding) - Fortran coding information
* [Compiling](#compiling) - compiling the software
* [Testing](#testing) - how to automate TSTool code testing
* [Deploying](#deploying) - building an installer and deploying an operational TSTool

---------------------

## Run Eclipse ##

Eclipse is run on Windows using the following batch file.
Other similar batch files and scripts can be created as needed to handle variations
in the development environment.

```
C:\Users\user\cdss-dev\TSTool\git-repos\cdss-app-tstool-main\build-util\run-eclipse-neon-32bit.bat`
```

## Designing Software ##

Software should be designed consistent with TSTool design standards.

* See the [Software Design](../software-design/overview) section.

## Version Control with Git ##

TSTool version control is consistent with CDSS protocols.

* See the [CDSS / Learn Git](http://learn.openwaterfoundation.org/cdss-learn-git/) documentation.

## Documenting ##

TSTool documentation should follow conventions of the developer and user documentation.

* See the [TSTool User Documentation repository](https://github.com/OpenWaterFoundation/cdss-app-tstool-doc-user)
* See the [TSTool Developer Documentation repository](https://github.com/OpenWaterFoundation/cdss-app-tstool-doc-dev)

## Troubleshooting Eclipse ##

**Need to include documentation.**

## Coding ##

**Need to include documentation about code standards.**

## Compiling ##

The Eclipse IDE automatically compiles code as changes are made.

## Testing ##

TSTool testing relies on extensive functional tests.

* See the [cdss-app-tstool-test test repository](https://github.com/OpenWaterFoundation/cdss-app-tstool-test)
* See the [Quality Control](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/quality-control/quality-control/) chapter of the TSTool documentation.

## Deploying ##

TSTool is distributed as a self-extracting installer.

**Need to describe here how to create the installer.**
