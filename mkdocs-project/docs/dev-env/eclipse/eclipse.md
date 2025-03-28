# TSTool / Development Environment / Eclipse #

*   [Introduction](#introduction)
*   ![Windows icon](../../images/windows-32.png) [Windows](#windows)
     +   [Download Eclipse 2022-06](#download-eclipse-2022-06)
     +   [Install Eclipse](#install-eclipse)
     +   [Check Eclipse Run Script](#check-eclipse-run-script)
*   ![Linux icon](../../images/linux-32.png) [Linux](#linux)

-----

## Introduction ##

The Eclipse Integrated Development Environment (IDE) has traditionally been used for TSTool software development and is recommended.
Alternate IDEs may be supported at some point; however, investigating impacts of using other IDEs
on TSTool development will require resources.
Eclipse does have some issues and limitations, but other IDEs have different issues.

TSTool development has typically occurred on Windows computers, although the software is often deployed to other operating systems.

As discussed in the [Development Environment / Java](../java/java.md) documentation,
OpenJDK Java 11 is currently used for development as of TSTool version 15.0.0.
The following table lists TSTool versions and Eclipse versions that have been used for development.

**<p style="text-align: center;">
TSTool Versions and Corresponding Eclipse Versions
</p>**

| **TSTool Version** | **Eclipse Version**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | **Comment** |
| -- | -- | -- |
| 15.0.0 | 4.24.0 (2022-06) | Installation is described in this documentation, last Eclipse version that runs with Java 11. |
| < 15.0.0 | 4.11.0 (2019-03) | See the [archived documentation](eclipse-2019-03/eclipse-2019-03.md). |
| Older versions (Mars, Neon, etc.) | | Not documented (obsolete). |

32-bit Java was previously used due to component requirements.
TSTool has been developed with various versions of Eclipse, including Mars, Neon, 2019-03 and later versions.
The version of Eclipse is generally not critical as long as the appropriate Java version is configured for compatibility.

The Eclipse `.project` file is currently saved in the Git repository for each TSTool component repository
in order to facilitate development environment setup.  This may change in the future.
Using a compatible version of Eclipse between developers ensures that the format of such files is consistent.

The Eclipse workspace (`.metadata`) folder is not saved in Git repository and is instead
is recommended to be saved in `eclipse-workspace` folder under the TSTool product folder
in a standard development folder structure.

## ![Windows icon](../../images/windows-32.png) Windows ##

### Download Eclipse 2022-06 ###

Download the 2022-06 version of Eclipse, which can be run with Java 11:

*   See the [Eclipse Packaging Project (EPP) Releases](https://www.eclipse.org/downloads/packages/release) web page.
*   Select the ***2022-06*** release.
*   Download the ***Eclipse IDE for Java Developers*** (there is currently no reason to use the Eclipse IDE for Java EE Developers,
    which is used for web development).  Select the ***Windows x86_64*** version.
*   The zip file installer is convenient because it is very clear where the software is installed.
    Save the zip file (e.g. `eclipse-java-2022-06-R-win32-x86_64.zip`) in the user's `Downloads` folder.

### Install Eclipse ###

To avoid confusion with other versions of Eclipse that may be installed on the computer
(as needed for other product development or during transition from one version of software to another),
install by copying/unzipping:

*   from zip file folder: `eclipse`
*   to: `C:\Program Files\Eclipse\eclipse-java-2022-06`

This helps distinguish the version as being for Java development
and allows multiple Eclipse versions to be installed on the computer.
The resulting folder structure is as shown in the following figure.

**<p style="text-align: center;">
![Eclipse software folders](images/eclipse-install-folder.png)
</p>**

**<p style="text-align: center;">
Eclipse Software Folders (<a href="../images/eclipse-install-folder.png">see full-size image</a>)
</p>**

### Check Eclipse Run Script ###

The `cdss-app-tstool-main` repository `build-util` folder contains scripts to run the correct version of Eclipse,
assuming a standard installation folder.  For example, `build-util/run-eclipse-win64.cmd` can be run from a Windows command shell.
This ensures that the proper versions of Eclipse and Java are used.
If necessary, this script can be modified or other versions added over time (for example for new versions of Java and Eclipse).

The Eclipse splash screen should show that the Eclipse version agrees with that installed above.
If not, make sure that the run script has been updated to run the correct version of Eclipse and that
Eclipse is installed in the correct location.

## ![Linux icon](../../images/linux-32.png) Linux ##

**This documentation has not been updated for Eclipse 2022-06 but should be OK.**

TSTool is typically developed on Windows, with Linux used for testing to ensure that features work on Linux.
The Linux environment is not the primary development or production environment,
although support for Linux is being increased over time.

The TSTool Linux development environment is consistent with the operating system and 64-bit is used by default.
The following documentation was prepared for Debian Stretch.

### Download Eclipse ###

The Eclipse Linux version is downloaded from the
[main Eclipse Download Page](https://www.eclipse.org/downloads/packages/release/neon/2/eclipse-ide-java-developers).
Unlike Windows, newer versions of Eclipse can be used,
at least Neon but later has also been used (for example 2019-09 release).
Save the download file, for example `~/Downloads/eclipse-inst-linux64.tar.gz`.

### Install Eclipse ###

The Eclipse installer from the previous step should be unzipped, for example:

```
$ cd ~/Downloads
$ tar -xzvf ~/media/vbshare/eclipse-inst-linux64.tar.gz
```

The top level folder is `eclipse-installer`.  The installer is run using:

```
$ cd eclipse-installer
$ ./eclipse-inst
```

The following images illustrate the installation process.

First pick ***Eclipse IDE for Java Developers***.
The following defaults are shown, based on Java 8 being installed and using the standard
installation folder.

**<p style="text-align: center;">
![Linux eclipse installer selection](images/linux-install-eclipse1.png)
</p>**

**<p style="text-align: center;">
Install Eclipse (<a href="../images/linux-install-eclipse1.png">see full-size image</a>)
</p>**

Press ***Install*** to install Eclipse.  Accept the license.
License certificates should also be accepted as shown below.

**<p style="text-align: center;">
![Linux install Eclipse, accept certificates](images/linux-install-eclipse2.png)
</p>**

**<p style="text-align: center;">
Install Eclipse - Accept Certificates (<a href="../images/linux-install-eclipse2.png">see full-size image</a>)
</p>**

After the software is installed, Eclipse can be launched from the installer.
However, a run script is typically configured as discussed in the following section.

### Check Eclipse Run Script ###

The `cdss-app-tstool-main` repository `build-util` folder contains scripts to run the correct version of Eclipse,
assuming a standard installation folder.
For example, `build-util/run-eclipse.bash` can be run from a Linux terminal.
This ensures that the proper versions of Eclipse and Java are used.
If necessary, this script can be modified or other versions added over time (for example for new versions of Java and Eclipse).
