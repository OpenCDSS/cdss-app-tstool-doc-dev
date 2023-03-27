# TSTool / Development Tasks / Deploying #

This documentation explains to to deploy the software and documentation to published locations.

*   [Deploy Software Installer](#deploy-software-installer)
*   [Deploy Documentation](#deploy-documentation)

---------------

## Deploy Software Installer ##

The installer that is created in the `dist` folder in the main TSTool repository is uploaded to the
OpenCDSS GCP cloud using the `build-util/copy-to-co-dnr-gcp.sh` script.
This script optionally allows updating an OpenCDSS index file listing all software installers on GCP.

## Deploy Documentation ##

The MkDocs user and developer documentation are deployed using `build-util/copy-to-co-dnr-gcp.sh` scripts
in the appropriate repositories.
