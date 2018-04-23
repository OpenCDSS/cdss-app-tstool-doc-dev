# TSTool / New Developer Setup / Overview #

This documentation is for software developers that are members of the core TSTool team and others who
have an interest in contributing to the TSTool software project.
It is recommended that the TSTool development environment should follow these setup instructions, which are
consistent with the [Development Environment](../dev-env/overview/) and [Initial Project Setup](../project-init/overview/) documentation.
The [standard development folder structure](../project-init/overview#development-files-structure)
should be followed to minimize potential for issues,
especially given the number of components and setup steps.
All of this documentation is consistent with the recommended development environment.

This documentation and development environment are also consistent with other CDSS Java software development environments.

The intent of this documentation is to completely document setup steps and allow new developers to comment on this documentation
so that it can be improved for other developers. The following steps need to occur to set up a new developer's environment.
Links to other documentation are included to provide more information and "(**see details below**)" is used to indicate that
specific instructions are included below (rather than immediately linking to other pages from the following outline).
After reading instructions for a step, use "back" to return to this outline so that setup instructions can be followed in the proper sequence.
**Bold comments** indicate which steps are required and which are optional.

1. **Required:** [Machine for Development](../dev-env/machine) - need a suitable computer
1. **Required:** [Create folder for development files](#create-folder-for-development-files) - where development will occur (**see details below**)
2. **Required (if not already installed):** Development Environment software install part 1 (version control)
	* [Development Environment / Git](../dev-env/git/) - install Git software so the repository can be cloned
3. **Required:** [Clone Git Repositories](#clone-git-repositories) - clone the repositories to get access to all files (**see details below**)
4. **Optional:** Development Environment software install part 2 (documentation tools), **(install if will view and edit documentation within the development environment)**
	* [Development Environment / Python and pip](../dev-env/python/) - install Python, which is needed by MkDocs
	* [Development Environment / MkDocs](../dev-env/mkdocs/) - install MkDocs to view/edit full documentation locally.
	See [Development Tasks / Documenting](../dev-tasks/documenting#developer-documentation-using-mkdocs)
	for instructions on viewing documentation.
5. **Required:** Development Environment software install part 3 (Java development tools)
	* **Required:** [Development Environment / Java 8](../dev-env/java8/) - make sure Java 8 is available on system
	* **Required (if not already installed):** [Development Environment / Eclipse](../dev-env/eclipse/) - install Eclipse for use as IDE
	* **Optional:** [Development Environment / KDiff3](../dev-env/kdiff3/) - install software to facilitate comparing files
	**(highly useful and can be used with Git)**
6. **Required:** Eclipse Workspace Setup (interactive development environment)
	* **Required:** [Create Eclipse Workspace Folder](#create-eclipse-workspace-folder) - simple manual step (***see details below***)
	* **Required:** [Import the Existing Eclipse TSTool Projects from the Git Repository Folders](#import-the-existing-eclipse-tstool-projects-from-the-git-repository-folders) -  import
	from Git repository working files (**see details below**)
7. [Next Steps - Development Tasks](#next-steps-development-tasks) - be productive!

The following sections are referenced from the above outline.

-------------

## Create Folder for Development Files ##

Create a development home folder consistent with the [initial project setup](../project-init/home-folder/) - this
is an umbrella folder for all TSTool development files,
including software tools that are installed locally (as appropriate).
It is assumed that development will occur within a developer's home folder on the computer in order to provide separation from the
work of other developers on the computer.
Tools such as Git rely on a unique identity for developers in order to properly track edits to files
and working in a shared space can be problematic.
After the folder is created, additional instructions describe how to install development files into the folder.

### ![Cygwin](../images/cygwin-32.png) Cygwin ###

[Cygwin](../resources#cygin) is a useful software platform to provide Linux programs on a Windows computer.
It may be convenient to use Cygwin for some work, such as running command-line utilities.
Do the following using a terminal window. Note that the syntax `~` indicates the home folder and is equivalent to the `$HOME` environment
variable location.
The following uses the Windows location for user files (rather than Cygwin location),
which allows Eclipse and other tools to work in Windows on the files accessed via Cygwin.

```bash
$ cd /cygdrive/c/Users/user
$ mkdir cdss-dev
$ cd cdss-dev/
$ mkdir TSTool
```

### ![Linux](../images/linux-32.png) Linux ###

Do the following using a terminal window. Note that the syntax `~` indicates the home folder and is equivalent to the `$HOME` environment
variable location.

```bash
$ cd
$ mkdir cdss-dev
$ cd ~/cdss-dev/
$ mkdir TSTool
```

### ![Windows](../images/windows-32.png) Windows ###

Do the following in a Windows command shell, Git CMD, or perform the equivalent actions in file explorer, or Git Bash.

```com
> C:
> cd \Users\userName
> mkdir cdss-dev
> cd cdss-dev
> mkdir TSTool
```

*Press back in the browser to return to the outline.*

## Clone Git Repositories ##

The GitHub repositories described in the [Software Design section](../software-design/overview) contain various components needed for TSTool development.
Each repository will be cloned into a local folder.

If Eclipse is used, the repositories will be imported into the Eclipse workspace as Java projects (code) and general projects.

If prompted when using `git clone`, specify the GitHub account credentials.

### ![Cygwin](../images/cygwin-32.png) Clone the repository files (Cygwin) ###

Follow the instructions for Linux but change the first step to the following to ensure that
the shared Cygwin/Windows file location is used.

```bash
$ cd /cygdrive/c/Users/user/cdss-dev/TSTool
```

### ![Linux](../images/linux-32.png) Clone the repository files (Linux) ###

```bash
$ cd ~/cdss-dev/TSTool
$ mkdir git-repos
$ cd git-repos
$ git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-doc.git
$ git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-doc-dev.git
$ git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-doc-user.git
$ git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-main.git
$ git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-test.git
$ git clone https://github.com/OpenWaterFoundation/cdss-lib-cdss-java.git
$ git clone https://github.com/OpenWaterFoundation/cdss-lib-common-java.git
$ git clone https://github.com/OpenWaterFoundation/cdss-lib-dmi-hydrobase-java.git
$ git clone https://github.com/OpenWaterFoundation/cdss-lib-dmi-nwsrfs-java.git
$ git clone https://github.com/OpenWaterFoundation/cdss-lib-dmi-riversidedb-java.git
$ git clone https://github.com/OpenWaterFoundation/cdss-lib-dmi-satmonsys-java.git
$ git clone https://github.com/OpenWaterFoundation/cdss-lib-models-java.git
$ git clone https://github.com/OpenWaterFoundation/cdss-lib-processor-ts-java.git
$ git clone https://github.com/OpenWaterFoundation/cdss-util-buildtools.git
```

### ![Windows](../images/windows-32.png) Clone the repository files (Windows) ###

```com
> C:
> cd \Users\user\cdss-dev\TSTool
> mkdir git-repos
> cd git-repos
> git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-doc.git
> git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-doc-dev.git
> git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-doc-user.git
> git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-main.git
> git clone https://github.com/OpenWaterFoundation/cdss-app-tstool-test.git
> git clone https://github.com/OpenWaterFoundation/cdss-lib-cdss-java.git
> git clone https://github.com/OpenWaterFoundation/cdss-lib-common-java.git
> git clone https://github.com/OpenWaterFoundation/cdss-lib-dmi-hydrobase-java.git
> git clone https://github.com/OpenWaterFoundation/cdss-lib-dmi-nwsrfs-java.git
> git clone https://github.com/OpenWaterFoundation/cdss-lib-dmi-riversidedb-java.git
> git clone https://github.com/OpenWaterFoundation/cdss-lib-dmi-satmonsys-java.git
> git clone https://github.com/OpenWaterFoundation/cdss-lib-models-java.git
> git clone https://github.com/OpenWaterFoundation/cdss-lib-processor-ts-java.git
> git clone https://github.com/OpenWaterFoundation/cdss-util-buildtools.git
```
The resulting files should match the [Development Files Structure](../project-init/overview#development-files-structure).

*Press back in the browser to return to the outline.*

## Create Eclipse Workspace Folder ##

This step is the same as the [Initial Project Setup](../project-init/eclipse-workspace/) so follow those instructions.
The Eclipse workspace folder for different environments is as follows:

* ![Cygwin](../images/cygwin-32.png) Linux:  the workspace folder is `/cygdrive/c/Users/user/cdss-dev/TSTool/eclipse-workspace`
* ![Linux](../images/linux-32.png) Linux:  the workspace folder is `~/cdss-dev/TSTool/eclipse-workspace`
* ![Windows](../images/windows-32.png) Windows: the workspace folder is `C:\Users\user\cdss-dev\TSTool\eclipse-workspace`

Start Eclipse by running the [Eclipse run script](../project-init/eclipse-run-script) as shown below.
This script can be used any time to run Eclipse for this project.
If it is necessary to modify this script,
[see recommendations for a developer-specific run script](../project-init/eclipse-run-script#developer-specific-run-script).

Open the workspace in Eclipse in preparation of adding the code project from the Git repository in the next step.

### ![Windows](../images/windows-32.png) Windows ###

```bash
> C:
> cd \Users\user\cdss-dev\TSTool\git-repos\cdss-app-tstool-main\build-util
> run-eclipse-neon-win32.bat
```

*Press back in the browser to return to the outline.*

## Import the Existing Eclipse TSTool Projects from the Git Repository Folders ##

**TODO smalers 2017-10-24 need to update for TSTool - see StateCU**

## Next Steps - Development Tasks ##

At this point it should be possible to [compile and run TSTool within the Eclipse interface](../dev-tasks/compiling).
See also:

* [Deployed Environment / Overview](../deployed-env/overview/) - for an overview of the deployed software
* [Software Design / Overview](../software-design/overview/) - to understand software structure and logic
* [Development Tasks / Overview](../dev-tasks/overview/) - common development tasks
