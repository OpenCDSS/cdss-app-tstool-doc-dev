# TSTool / Development Environment / launch4j ##

launch4j software is used to create an executable that wraps the Java Runtime Environment (JRE).

*   [launch4j Installation](#launch4j-installation)
*   [launch4j Configuration](#launch4j-configuration)

----

## launch4j Installation ##

To facilitate use, launch4j has been previously installed in the `cdss-util-buildtools` repository in
folder `lib/launch4j` and does not require any additional installation steps.
The `cdss-util-buildtools` scripts will use launch4j to build the software installer.
The following is the download page for launch4j in order to evaluate whether updates should be adopted.

*   [launch4j on SourceForge](https://sourceforge.net/projects/launch4j/)

## launch4j Configuration ##

The luanch4j software uses a file `bin/TSTool.l4j.ini` in the TSTool installation folder,
which is version-controlled in the `cdss-app-tstool-main` repository in folder `installer/common` folder.
This is used by launch4j at run-time to configure the Java Runtime Environment.
The following command line parameters are used by default, but can be changed after the software is intalled:

|**Parameter**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|**Description**|
|--|--|
|`-Xmx1170m`                       |Maximum memory for the Java virtual machine.  A memory maximum of 1170MB is appropriate for a 32-bit runtime environment and can be increased if a 64-bit JRE is used at run-time.  32-bit Java was used while mainly because of historical support for old Windows operating systems and use of native 32-bit libraries for HEC-DSS integration.  A 64-bit implementation is now available and there should be no reason to use the older 32-bit TSTool implementations.  The theoretical limit for memory on a 32-bit system is 4GB.  However, quite a bit of memory is taken by the virtual machine and a practical limit is 1.4GB.|
|`-Dsun.java2d.noddraw=true`       |Use to fix problems in graphics card drivers (sometimes have visual artifacts strewn about).|
|`-Djava.net.useSystemProxies=true`|Ensure that TSTool picks up on system firewall settings that may limit normal HTTP traffic for web services.|
