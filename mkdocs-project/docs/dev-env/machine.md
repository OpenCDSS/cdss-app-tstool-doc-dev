# TSTool / Development Environment / Machine ##

TSTool software development and testing can be resource-intensive.
It is recommended that a good computer is used in order to minimize issues.
Development has traditionally occurred on Windows 7 and 10 computers,
with deployment to Windows and Linux.
Development on Linux computer should be possible.

* Windows:
	+ Windows 10 or 7
* Linux:
	+ Confirm that Java 8 is available as a distribution
        + Oracle Java has traditionally be used for development
        + Other Java distributions may be appropriate
* Memory: 8GB minimum, 16GB or 32GB will help improve performance
* Administrator privileges are required for initial setup and likely will be required
to install and configure additional software later, as well as to test installers

The Cygwin environment can be used to facilitate development on Windows, with the following constraints:

* Be aware that Cygwin is Linux environment running within a Windows environment.
* End of line can be an issue because some Cygwin programs default to Linux end of line
and do not transparently recognize Windows end of line.
* Most tasks that require Linux commands can be performed in Git Bash git client,
although some developers may prefer the more complete Cygwin development environment.
* A repository that is cloned with Cygwin by the developer should be manipulated with Cygwin Git.
A repository that is cloned with Git Bash or other windows Git client should be manipulated with the Windows Git client.
* Instructions related to Cygwin are provided to facilitate command line tools and automation.
* **Eclipse is typically not installed within Cygwin.**
