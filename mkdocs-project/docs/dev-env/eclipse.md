# TSTool / Development Environment / Eclipse ##

* [Introduction](#introduction)
* ![Windows](../images/windows-32.png) [Windows](#windows)
	+ [Download Eclipse Neon](#download-eclipse-neon)
	+ [Install Eclipse Neon ](#install-eclipse-neon)
	+ [Check Eclipse Run Script](#check-eclipse-run-script)
* ![Linux](../images/linux-32.png) [Linux](#linux)

-----

## Introduction ##

The Eclipse Integrated Development Environment (IDE) has traditionally been used for TSTool software development and is recommended.
Alternate IDEs may be supported at some point; however, investigating impacts of using other IDEs
on TSTool development will require resources.
Eclipse does have some issues and limitations, but other IDEs have different issues.

TSTool development has typically occurred on Windows computers, although the software is often deployed to other operating systems.

As discussed in the [Java 8](java8.md) section,
Java 8 is currently used for development and 32-bit Java is used due to component requirements.
To avoid confusion with compatibility, Eclipse 32-bit has traditionally been used.
However, the Eclipse foundation has begun phasing out 32-bit Java and 64-bit Eclipse
will be used when TSTool is transitioned to 64-bit Java.
TSTool has been developed with various versions of Eclipse, including Mars and Neon.

The Eclipse `.project` file is currently saved in the Git repository for each TSTool component repository
in order to facilitate development environment setup.  This may change in the future.
Using a compatible version of Eclipse between developers ensures that the format of such files is consistent.

The Eclipse workspace (`.metadata`) folder is not saved in Git repository and is instead
is recommended to be saved in `eclipse-workspace` folder under the TSTool product folder
in a standard development folder structure.

## ![Windows](../images/windows-32.png) Windows ##

### Download Eclipse Neon ###

The download links for Eclipse may change as new versions are released.  Search for "download eclipse neon", which indicates that
downloads are available on the following site (or similar).
For example, this may return:

* [Eclipse Neon 3 Packages](http://www.eclipse.org/downloads/packages/release/Neon/3)

Download the ***Eclipse IDE for Java Developers*** (there is currently no reason to use the Eclipse IDE for Java EE Developers,
which is used for web development).  Make sure to select the ***Windows 32-bit*** version.
The zip file is convenient because it is very clear where the software is installed.

### Install Eclipse Neon ###

The Eclipse Neon installer file will be named `eclipse-java-neon-3-win32.zip` or similar.
Note that later versions of Eclipse provide an installation program so these instructions need to be updated when later versions of Eclipse are used.

To avoid confusion with other versions of Eclipse that may be installed on the computer (as needed for other product development),
install by copying/unzipping into a folder named `C:\Program Files (x86)\eclipse-java-neon-3-win32`.
The resulting folder structure is as shown in the following figure.
This is a bit redundant withe the extra `eclipse` folder but clearly indicates the version and preserves the folder names from the zip file distribution.

**<p style="text-align: center;">
![eclipse-install-folder](images/eclipse-install-folder.png)
</p>**

**<p style="text-align: center;">
Eclipse Software Folders (<a href="../images/eclipse-install-folder.png">see full-size image</a>)
</p>**

### Check Eclipse Run Script ###

The `cdss-app-tstool-main` repository `build-util` folder contains scripts to run the correct version of Eclipse,
assuming a standard installation folder.  For example, `build-util/run-eclipse-win32.bat` can be run from a Windows command shell.
This ensures that the proper versions of Eclipse and Java are used.
If necessary, this script can be modified or other versions added over time (for example for new versions of Java and Eclipse).

## ![Linux](../images/linux-32.png) Linux ##

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
![linux-install-eclipse1](images/linux-install-eclipse1.png)
</p>**

**<p style="text-align: center;">
Install Eclipse (<a href="../images/linux-install-eclipse1.png">see full-size image</a>)
</p>**

Press ***Install*** to install Eclipse.  Accept the license.
License certificates should also be accepted as shown below.

**<p style="text-align: center;">
![linux-install-eclipse2](images/linux-install-eclipse2.png)
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
