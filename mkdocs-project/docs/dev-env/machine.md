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
* Administrator privileges will be required for initial setup and likely will be required
to install and configure additional software later, as well as to test installers

The Cygwin environment can be used to facilitate development on Windows, with the following constraints:

* Be aware that Cygwin is Linux environment running within a Windows environment.
* End of line can be an issue because some Cygwin programs default to Linux end of line
and do not transparently recognize Windows end of line.
* Instructions related to Cygwin are purely to facilitate command line tools.
**Eclipse is typically not installed within Cygwin.**
