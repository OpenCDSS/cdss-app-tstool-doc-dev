# TSTool / Development Environment / Machine #

*   [Introduction](#introduction)
*   [Development Machine Requirements](#development-machine-requirements)
*   [Use of Git Bash](#use-of-git-bash)
*   [Use of Cygwin](#use-of-cygwin)

-----

## Introduction ##

TSTool software development and testing can be resource-intensive.
It is recommended that a good computer is used to minimize issues.
Development has occurred on Windows computers with deployment to Windows and Linux.
Development on a Linux computer or virtual machine is possible.

## Development Machine Requirements ##

*   Windows:
    +   Windows 10+
*   Linux:
    +   Confirm that Java 11 is available as a distribution (or later Java depending on TSTool version):
        -   see the [Development Environment / Java](java/java.md) documentation for Java version information
        -   OpenJDK Java is used for development and releases
        -   Other Java distributions may be appropriate
*   Memory: 8GB minimum, 16GB or 32GB will help improve performance.
*   Disk space: Software tools and development typically require several GB of storage.
*   Administrator privileges are required for initial setup and likely will be required
    to install and configure additional software later, as well as to test installers.

## Use of Git Bash ##

This documentation recommends installing Git for Windows, which includes Git Bash.
Git Bash provides a Linux shell running in Windows.
Git Bash scripts are used for some automated tasks.
Creating files in Git Bash results in end of line characters that are consistent with Windows,
which tends to avoid issues seen with Cygwin (see the next section).

## Use of Cygwin ##

The Cygwin environment can be used to facilitate development on Windows, with the following constraints:

*   Be aware that Cygwin is Linux environment running within a Windows environment.
*   End of line can be an issue because some Cygwin programs default to Linux end of line
    and do not transparently recognize Windows end of line.
*   Most tasks that require Linux commands can be performed in Git Bash git client,
    although some developers may prefer the more complete Cygwin development environment.
*   A repository that is cloned with Cygwin by the developer should be manipulated with Cygwin Git.
    A repository that is cloned with Git Bash or other windows Git client should be manipulated with the Windows Git client.
*   Instructions related to Cygwin are provided to facilitate command line tools and automation.
*   **Eclipse is typically not installed within Cygwin.**
