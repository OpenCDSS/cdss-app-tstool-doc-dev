# TSTool / Development Tasks / Deploying #

This documentation explains to to deploy the software and documentation to published locations.

* [Deploy Software Installer](#deploy-software-installer)
* [Deploy Documentation](#deploy-documentation)

---------------

## Deploy Software Installer ##

The installer that is created in the `dist` folder in the main TSTool repository has in the past been deployed to the
[Google Sites CDSS Staging page](https://sites.google.com/site/cdssstaging/tstool/download) that OWF created in 2013.
Old installers can be migrated to the OpenCDSS Google Cloud Platform website,

The GitHub repository ***Releases*** could also be used to upload installers,
although using the OpenCDSS Google Cloud Platform site may be cleaner.

## Deploy Documentation ##

The MkDocs user and developer documentation should be deployed according to the instructions in those repositories.
Generally this will involve running a script in the `build-util` folder to upload the static website content to the cloud location(s).
