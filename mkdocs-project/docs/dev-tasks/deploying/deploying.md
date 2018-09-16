# TSTool / Development Tasks / Deploying #

This documentation explains to to deploy the software and documentation to published locations.

* [Deploy Software Installer](#deploy-software-installer)
* [Deploy Documentation](#deploy-documentation)

---------------

## Deploy Software Installer ##

The installer that is created in the `dist` folder in the main TSTool repository has in the past been deployed to the
[Google Sites CDSS Staging page](https://sites.google.com/site/cdssstaging/tstool/download) that OWF created in 2013.
However, this site needs to be migrated to a CDSS/OpenCDSS website (waiting on State to establish),
perhaps with continued backup on the [new OWF software website](http://software.openwaterfoundation.org/).

The GitHub repository ***Releases*** tool should also be used to upload installers.
Releases can also be used for intermediate releases for third-party testing
but public releases on the CDSS website don't need to include all intermediate releases.

## Deploy Documentation ##

The MkDocs user and developer documentation should be deployed according to the instructions in those repositories.
Generally this will involve running a script in the `build-util` folder to upload the static website content to the cloud location(s).
