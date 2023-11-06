# TSTool / Development Environment / Java #

*   [Introduction](#introduction)
*   ![Windows icon](../images/windows-32.png) [Windows](#windows)
    +   [Download OpenJDK Java 8](#download-openjdk-java-8)
    +   [Install OpenJDK Java 8](#install-openjdk-java-8)
    +   [Create Symbolic Links for OpenJDK Java 8](#create-symbolic-links-for-openjdk-java-8)
    +   [Confirm OpenJDK Java 8 Eclipse Run Script Configuration](#confirm-openjdk-java-8-eclipse-run-script-configuration)
*   ![Linux icon](../images/linux-32.png) [Linux](#linux)

------

## Introduction ##

TSTool is written in Java and therefore the following Java software must be installed:

*   Java Development Kit (JDK) environment for development
*   Java Runtime Environment (JRE) for development and deployed environments

The primary development environment is Windows.
The Windows files are used to create the Linux installer.

The following table summarizes the Java version that is used with TSTool.

**<p style="text-align: center;">
TSTool and Related Java Versions
</p>**

| **TSTool Version** | **Java Version** | **Comment** |
| -- | -- | -- |
| 14.9.0 | OpenJDK Java 8 64-bit | Oracle began charging a fee for Java as of January 2019 and the OpenJDK Java distribution is used to avoid fees and allow updates. The initial OpenJDK version will be updated as resources allow and automated tests pass. |
| 14.0.0 | Oracle Java 8 64-bit. | This was a major update to move to 64-bit. |
| Before 14.0.0 | Oracle Java 8 32-bit and older. | 32-bit was used to support older versions of Windows. |
| Older versions | Older 32-bit Java versions. | See the release notes for a history of updates. |

32-bit Java was previously used and was necessary to support native libraries used by some TSTool features,
in particular the HEC-DSS libraries, which are used by `ReadHecDss` and `WriteHecDss` commands.
64-bit versions of these libraries were later integrated with TSTool to fully support 64-bit development environment.
**OpenJDK 64-bit Java is now the standard for TSTool.**

If necessary, it is possible to change the run-time Java for deployed TSTool software by swapping
the Java Runtime Environment (JRE) that is distributed with TSTool.
On Windows, replace the `jre_18` folder with a different Java version.
On Linux, the `bin/tstool` run script searches for the most recent supported version of Java.

The remainder of this documentation describes the latest supported development environment.

## ![Windows icon](../images/windows-32.png) Windows ##

The Java development and runtime environment has changed over time:

*   Java 8 (OpenJDK):
    +   OpenJDK Java 8 (current development environment) - see below
*   Java 8:
    +   [Oracle Java 8](java8-oracle.md) - used for TSTool 14.8.6 and earlier,
        and will be archived for a while
*   Java 7 and earlier:
    +   not documented here but is mentioned in release notes

Newer Java versions will be used in future TSTool releases.

### Download OpenJDK Java 8 ###

As of TSTool 14.9.0, TSTool is developed using OpenJDK Java.
OpenJDK is published by the OpenJDK project.
Other organizations provide enhanced versions that differ from the original OpenJDK versions and will be found
when searching for "OpenJDK downloads".
TSTool is developed using the standard OpenJDK version.

OpenJDK versions are archived and are available for download.
Unfortunately, downloads for OpenJDK can be confusing because the Oracle website does not
always use "OpenJDK" in URLs and content, and packaging for download is minimal.

See the following resources:

*   Oracle website:
    +   [OpenJDK: How to download and install prebuilt OpenJDK packages](https://openjdk.org/install/) - general instructions
    +   [Archived OpenJDK General-Availability Releases](https://jdk.java.net/archive/) - includes versions 9+
        -   The downloads include the Java Development Kit (JDK) but do not contain a separate `jre` folder
            for the Java Runtime Environment (JRE) used in deployed systems
*   AdoptOpenJDK:
    *   [AdoptOpenJDK](https://adoptopenjdk.net/releases.html) - OpenJDK download page

Use the above AdoptOpenJDK page to select the required OpenJDK version.
For example, select "OpenJDK 8 (LTS)" and "Hotspot" to download Java 8 JDK and JRE.
Make sure to download the Windows x64 bit version for 64-bit Java.
Download the `.zip` (rather than the `.msi`) file to allow more control of the installation.
The download file will have a name similar to `OpenJDK8U-jdk_x64_windows_hotspot_8u382b05.zip`
for Java 8 update `382` and build `05`, and will have contents similar to the following.
Note that the zip file contains a `jre` folder that can be distributed in the deployed environment and the `src`
folder contains unneeded source code.

**<p style="text-align: center;">
![OpenJDK Java 8 zip file contents](images/openjdk-java8/java8-1-zipfiles.png)
</p>**

**<p style="text-align: center;">
OpenJDK Java 8 Zip File Contents (<a href="../images/openjdk-java8/java8-1-zipfiles.png">see full-size image</a>)
</p>**

The packaging for files changed with Java 9.  The following image shows the main zip file contents for
OpenJDK 9 download file `OpenJDK9U-jdk_x64_windows_hotspot_9.0.4_11.zip`.
Note that there is no `jre` folder for the Java Runtime Environment.

**<p style="text-align: center;">
![OpenJDK Java 9 JDK zip file contents](images/openjdk-java8/java9-1-zipfiles.png)
</p>**

**<p style="text-align: center;">
OpenJDK Java 9 JDK Zip File Contents (<a href="../images/openjdk-java8/java9-1-zipfiles.png">see full-size image</a>)
</p>**

The AdoptOpenJDK download page provides a separate download for JRE (the Oracle downloads page does not provide JRE downloads).
For example the `OpenJDK9U-jre_x64_windows_hotspot_9.0.4_11.zip` file contents are as follows:

**<p style="text-align: center;">
![OpenJDK Java 9 JRE zip file contents](images/openjdk-java8/java9-2-jre-zipfiles.png)
</p>**

**<p style="text-align: center;">
OpenJDK Java 9 JRE Zip File Contents (<a href="../images/openjdk-java8/java9-2-jre-zipfiles.png">see full-size image</a>)
</p>**

### Install OpenJDK Java 8 ###

The zip file(s) described in the previous section contain the necessary Java files that
can be copied to the appropriate location on the Windows computer.

For Java 8:

*   Copy the main Java folder (e.g., `jdk8u382-b05`) to `C:\Program Files\Java\jdk8u382-b05`).
*   Because the `jre` folder exists in the above folder, no additional copy is needed
    (an extra copy step is required for Java 9 and later).

The following shows older Oracle JDK (`jdk1.8.0_191`) and JRE installations with the newer OpenJDK folder (`jdk8u382-b05`).
The other folders are links that are described in the next section.

**<p style="text-align: center;">
![Java program folders](images/openjdk-java8/java8-2-program-files.png)
</p>**

**<p style="text-align: center;">
Java Program Files (<a href="../images/openjdk-java8/java8-2-program-files.png">see full-size image</a>)
</p>**

### Create Symbolic Links for OpenJDK Java 8 ###

The folder containing the OpenJDK Java 8 files (`C:\Program Files\Java\jdk8u382-b05`) will be used by the Eclipse software during development,
and the JRE folder will be packaged with the TSTool installer.

The use of version-specific folder can be problematic because Eclipse Java Runtime Environment and build utilities must
be configured to use the specific version.
This may result in developers with different minor versions of Java flip-flopping repository contents.
To minimize such issues, links with generic names are created.
See the previous section for am image that illustrates the links.

If old versions of Java software exist that will not be used by other software:

*   remove old links using File Explorer,
    which will remove the links without removing the original folders.
*   rename the old folders, for example with a leading `x-` to ensure that they are not used in the development environment
    (this will break any references to the old versions,
    so it may be necessary to keep the names if other software is using the old versions)
*   if the old versions are no longer needed, they can be removed

To create new links,
open a Windows command shell with Administrator privileges and create symbolic links as shown in the following image and
summarized below.
**Exclipse seems to traverse the link and use the specific resource in its environment, showing the full path rather than the link,
but it is convenient nevertheless and is needed for scripts that use general folder names.**

```
cd \Program Files\Java
mklink /d jdk8 jdk8u382-b05
mklink /d jre8 jdk8u382-b05\jre
```

In addition, the automated build system uses JRE folder that requires another symbolic link to find the JRE to distribute with the installer.
Create the link as follows in the `C:\Program Files\Java` folder:

```
mklink /d jre_18 jdk8u382-b05\jre
```

The resulting `C:\Program Files\Java` folder will have contents similar to the following:

**<p style="text-align: center;">
![Java program folders](images/openjdk-java8/java8-3-program-files-links.png)
</p>**

**<p style="text-align: center;">
Java Program Files (<a href="../images/openjdk-java8/java8-3-program-files-links.png">see full-size image</a>)
</p>**

If Eclipse has been configured (see the [Eclipse](eclipse.md) configuration),
the Eclipse ***Window / Preferences*** menu can be used to check what version of Java is being used.
See the ***Java / Installed JREs*** preferences, which should look similar to the following (note the general `jdk8` folder name).

**<p style="text-align: center;">
![Eclipse Java interpreter preferences](images/openjdk-java8/java8-4-eclipse-preferences.png)
</p>**

**<p style="text-align: center;">
Java Program Files (<a href="../images/openjdk-java8/java8-4-eclipse-preferences.png">see full-size image</a>)
</p>**

To check the Java version being used at runtime in TSTool,
use the ***Help / About TSTool*** menu and then press the ***Show Software / System Details*** button, which will show the following.

*   `java.vendor = Temurin`
*   `java.vendor.url = https://adoptium.net` - for AdoptOpenJDK
*   `java.version = 1.8.0_382` - should match the Java version configured above

**<p style="text-align: center;">
![TSTool Java Runtime Properties](images/openjdk-java8/java8-5-runtime-properties.png)
</p>**

**<p style="text-align: center;">
TSTool Java Runtime Properties (<a href="../images/openjdk-java8/java8-5-runtime-properties.png">see full-size image</a>)
</p>**

### Confirm OpenJDK Java 8 Eclipse Run Script Configuration ###

The order that Java and Eclipse are installed may vary.
These major development environment components need to be configured appropriately and it is useful to use a run script to start Eclipse.

*   [See information about the Eclipse run script](eclipse.md#check-eclipse-run-script) - ensures that a standard development environment is used

## ![Linux icon](../images/linux-32.png) Linux ##

This documentation was prepared while installing TSTool for Java 8 on a Debian Stretch Linux VirtualBox virtual machine.
Other environments will be similar, using a Java version that is required for the TSTool version.

Java 8 was installed using the following command:

```
$ sudo apt-get install openjdk-8-jdk
```
