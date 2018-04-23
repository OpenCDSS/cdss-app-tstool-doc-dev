# TSTool / Initial Project Setup / Overview ##

This documentation describes the project initialization.
This information is provided in case the software project needs to be
re-initialized, and to provide rationale for how the project was set up.

* [Development Files Structure](#development-files-structure)

------------------

## Development Files Structure ##

This documentation assumes that files are configured according to the following file structure.
It is recommended that TSTool developers follow this file organization closely because if they do not,
the documentation will be less helpful and troubleshooting will require additional resources.
Feedback on the structure can be discussed with the development team leads.
The structure is similar on Linux and Windows, other than the top-level user folders.
Linux forward-slashes are used to indicate folders in the following.

```text
/home/user/                              Linux:  Software developer's home folder.
/cygdrive/C/Users/user/                  Cygwin:  Software developer's home folder.
C:\Users\user\                           Windows:  Software developer's home folder.
  cdss-dev/                              CDSS software products.
    TSTool/                              CDSS TSTool software product.
      eclipse-workspace/                 Eclipse workspace to organize Eclipse projects.
      git-repos/                         Git repositories that comprise TSTool.
        cdss-app-tstool-doc/             Legacy user documentation, some developer documentation.
        cdss-app-tstool-doc-dev/         New Markdown/MkDocs developer documentation.
        cdss-app-tstool-doc-user/        New Markdown/MkDocs user documentation.
        cdss-app-tstool-main/            Main TSTool application code.
          .git/                          Git local repository - DO NOT TOUCH DIRECTLY
          .gitattributes                 Git repository properties.
          .github/                       Folder containing issues template, etc., used by GitHub.
          .gitignore                     Git repository global ignore list.
          other files                    See details for each repository.
        cdss-app-tstool-test/            Functional tests using built-in test features.
        cdss-lib-cdss-java/              CDSS code components shared across CDSS applications.
        cdss-lib-common-java/            Utility code components shared across applications.
        cdss-lib-dmi-hydrobase-java/     API for Colorado's HydroBase database and web services.
        cdss-lib-dmi-nwsrfs-java/        Legacy API for National Weather Service River Forecast Center models.
        cdss-lib-dmi-riversidedb-java/   API for Riverside Technology Database.
        cdss-lib-dmi-satmonsys-java/     API for Colorado's Satellite Monitoring System.
        cdss-lib-models-java/            API for CDSS StateCU and StateMod models.
        cdss-lib-processor-ts-java/      API for TSTool command processor and commands.
        cdss-util-buildtools/            Utility programs to build TSTool installer.
```
