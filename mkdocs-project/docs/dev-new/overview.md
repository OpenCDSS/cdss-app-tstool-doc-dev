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
2. **Required:** [Create folder for development files](#create-folder-for-development-files) - where development will occur (**see details below**)
3. **Required (if not already installed):** Development Environment software install part 1 (version control)
	* [Development Environment / Git](../dev-env/git/) - install Git software so the repositories can be cloned
4. **Required:** [Clone Git Repositories](#clone-git-repositories) - clone the repositories to get access to all files (**see details below**)
5. **Required:** Development Environment software install part 2 (Java development tools)
	* **Required:** [Development Environment / Java 8](../dev-env/java8/) - make sure Java 8 is available on system
	* **Required (if not already installed):** [Development Environment / Eclipse](../dev-env/eclipse/) - install Eclipse for use as IDE
	* **Optional:** [Development Environment / KDiff3](../dev-env/kdiff3/) - install software to facilitate comparing files
	**(highly useful and can be used with Git)**
	* **Optional:** [Development Environment / NSIS](../dev-env/nsis/) - install software to create TSTool software installer
6. **Required:** Eclipse Workspace Setup (interactive development environment)
	* **Required:** [Create Eclipse Workspace Folder](#create-eclipse-workspace-folder) - simple manual step (***see details below***)
	* **Required:** [Import the Existing Eclipse TSTool Projects from the Git Repository Folders](#import-the-existing-eclipse-tstool-projects-from-the-git-repository-folders) -  import
	from Git repository working files (**see details below**)
7. **Optional:** Development Environment software install part 3 (documentation tools), **(install if will view and edit documentation within the development environment)**
	* [Development Environment / Python and pip](../dev-env/python/) - install Python, which is needed by MkDocs
	* [Development Environment / MkDocs](../dev-env/mkdocs/) - install MkDocs to view/edit full documentation locally.
	See [Development Tasks / Documenting](../dev-tasks/overview#documenting)
	for instructions on viewing documentation.
8. [Next Steps - Development Tasks](#next-steps-development-tasks) - be productive!

The following sections are referenced from the above outline.

-------------

## Create Folder for Development Files ##

Create a development home folder consistent with the [initial project setup](../project-init/overview) - this
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
Do the following using a terminal window. Note that the syntax `~` indicates the home folder for Bash shell
and is equivalent to the `$HOME` environment variable location.
The following uses the Windows location for user files (rather than Cygwin location `/home/user`,
which are typically stored in the Windows Cygwin install folder `C:\cygwin64\home` folder),
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

The GitHub repositories described in the [standard development folder structure](../project-init/overview#development-files-structure)
contain various components needed for TSTool development.
Each repository will be cloned into a local folder.

If Eclipse is used, the repositories will be imported into the Eclipse workspace as Java projects (code) and general projects.

If prompted when using `git clone`, specify the GitHub account credentials.

### ![Cygwin](../images/cygwin-32.png) Clone the repository files (Cygwin) ###

Follow the instructions for Linux (see below) but change the first step to the following to ensure that
the shared Cygwin/Windows file location is used.

```bash
$ cd /cygdrive/c/Users/user/cdss-dev/TSTool
```

### ![Linux](../images/linux-32.png) Clone the repository files (Linux) ###

The following assumes that the Bash shell is used.
If the `~` notation is not recognized as the home folder, use `$HOME`.

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

This step creates the `eclipse-workspace` workspace folder where Eclipse saves its files to manage the TSTool software, 
as discussed in the [Development Files Structure](../project-init/overview#development-files-structure).

The recommended Eclipse workspace folder for different environments is as follows:

* ![Cygwin](../images/cygwin-32.png) Linux:  the workspace folder is `/cygdrive/c/Users/user/cdss-dev/TSTool/eclipse-workspace`
* ![Linux](../images/linux-32.png) Linux:  the workspace folder is `~/cdss-dev/TSTool/eclipse-workspace`
* ![Windows](../images/windows-32.png) Windows: the workspace folder is `C:\Users\user\cdss-dev\TSTool\eclipse-workspace`

Start Eclipse by running the [Eclipse run script](../project-init/eclipse-run-script) as shown below.
This script can be used any time to run Eclipse for this project.

Open the workspace in Eclipse in preparation of adding the code project from the Git repository in the next step.

### ![Windows](../images/windows-32.png) Windows ###

```bash
> C:
> cd \Users\user\cdss-dev\TSTool\git-repos\cdss-app-tstool-main\build-util
> run-eclipse-neon-3-win32.bat
```

Select a workspace as shown in the following figure.
If the `eclipse-workspace` folder was not created previously, it can be created via the eclipse dialog.

![eclipse-workspace-select](images/eclipse-workspace-select.png)

The Eclipse workspace folder is identified by a `.metadata` folder, which will be hidden on Linux.

*Press back in the browser to return to the outline.*

## Import the Existing Eclipse TSTool Projects from the Git Repository Folders ##

The TSTool repositories each correspond to discrete components that must be imported into the TSTool Eclipse workspace.
The development environment does not currently use Maven.
Eclipse `.project` files are committed to each repository, which allows the repository folders to be imported and be recognized as projects by Eclipse.
This approach may be changed as resources are allocated to evolving the development environment.

The repositories fall into four categories, which are discussed in the following sections.
All of the repositories obviously use Git for version control (Eclipse generally detects this automatically when a project is imported).

1. Code repositories with names ending with `java` are treated as Java projects.
2. The CDSS build utility repository `cdss-util-buildtools` is treated as a general project as is currently required to create the software installer.
3. The TSTool function test repository `cdss-app-tstool-test` is treated as a general project and is useful to import into Eclipse.
4. Documentation repositories with `doc` in names can be treated as general projects and do not need to be imported because their files are typically edited outside of Eclipse.

### Import Code Repositories ###

After the initial Eclipse workspace is selected, import the following repositories by following the same general procedure indicated below
(**images below have not been updated to include cdss-lib-dmi-hydrobase-rest-java component**):

* `cdss-app-tstool-main`
* `cdss-lib-cdss-java`
* `cdss-lib-common-java`
* `cdss-lib-dmi-hydrobase-java`
* `cdss-lib-dmi-hydrobase-rest-java`
* `cdss-lib-dmi-nwsrfs-java`
* `cdss-lib-dmi-riversidedb-java`
* `cdss-lib-dmi-satmonsys-java`
* `cdss-lib-models-java`
* `cdss-lib-processor-ts-java`

The initial workspace will be similar to the following.

![eclipse-worskpace-0](images/eclipse-workspace-0.png)

Because the `.project` files have already been created and are included in the repository,
a general import of existing project can occur, initiated with ***File / Import*** and as shown in the following figure:

![eclipse-workspace-1](images/eclipse-workspace-1.png)

Press ***Next >*** in the above dialog to continue to the following step.

![eclipse-workspace-3](images/eclipse-workspace-3.png)

All the existing projects can be added at once as shown in the following image.
Note that ***Copy projects into workspace*** is NOT checked.
This allows the files to exist in the Git repository folders.

Press ***Finish*** to start the import.
Eclipse will automatically try to compile TSTool and should properly handle project dependencies because
the `.classpath` file is also saved in each repository/project.
The default settings may not result in a full build; however, in the following image there were no fatal errors that prevented a build:

![eclipse-workspace-4](images/eclipse-workspace-4.png)

### Import Build Utility Repository ###

* `cdss-util-buildtools`

The above should have been imported as per the previous section.

### Import Test Repository ###

* `cdss-app-tstool-test`

The above should have been imported as per the previous section.

### Import Documentation Repositories (Optional) ###

Optionally, import the following documentation repositories using the procedure below.
It is not necessary to import the documentation repositories into Eclipse.
Doing so is somewhat useful in that Eclipse can provide access to files and use Git to manage the files.
However, a separate Git client can also be used.

* `cdss-app-tstool-doc`
* `cdss-app-tstool-doc-dev`
* `cdss-app-tstool-doc-user`

The first item above should have been imported as per the previous section, because it has traditionally been an Eclipse project.
However, the other two are new repositories that have not been saved as Eclipse projects.
It is OK to not import the last two repositories into Eclipse.

## Next Steps - Development Tasks ##

At this point it should be possible to [compile](../dev-tasks/overview#compiling) and
[run](../dev-tasks/overview#running) TSTool within the Eclipse interface].  See also:

* [Deployed Environment / Overview](../deployed-env/overview/) - for an overview of the deployed software
* [Software Design / Overview](../software-design/overview/) - to understand software structure and logic
* [Development Tasks / Overview](../dev-tasks/overview/) - common development tasks
