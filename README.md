# cdss-app-tstool-doc-dev #

This repository contains the developer documentation for Colorado's Decision Support Systems (CDSS) TSTool software.
The documentation uses Markdown format and MkDocs software to create a static website.

See the following online resources:

*   Latest deployed [CDSS / TSTool (Developer)](https://opencdss.state.co.us/tstool/latest/doc-dev/) documentation
*   [Colorado's Decision Support System (CDSS)](https://cdss.colorado.gov/)
*   [OpenCDSS](https://opencdss.state.co.us/opencdss/)
*   [TSTool software main repository](https://github.com/OpenCDSS/cdss-app-tstool-main)
*   [TSTool User Documentation](https://opencdss.state.co.us/tstool/latest/doc-user/)

See the following sections in this page:

*   [TSTool Software Overview](#tstool-software-overview)
*   [Repository Contents](#repository-contents)
*   [Development Environment](#development-environment)
*   [Editing and Viewing Content](#editing-and-viewing-content)
*   [Style Guide](#style-guide)
    +   [Web Accessibility](#web-accessibility)
*   [License](#license)
*   [Contributing](#contributing)
*   [Maintainers](#maintainers)
*   [Contributors](#contributors)
*   [Release Notes](#release-notes)

---------------------------

## TSTool Software Overview ##

The TSTool software is a Java application that automates time series processing:

1.  Command-based workflow language.
2.  General commands including as file manipulation, logic controls such as `For` and `If` commands,
    and support for processor properties to allow dynamic scripting.
3.  Time series data processing commands for:
    1.  Reading time series from files, databases, and web services
    2.  Creating time series
    3.  Setting time series data
    4.  Filling time series data
    5.  Manipulating time series data (add, multiply, etc.)
    6.  Analyzing time series
    7.  Models that use time series (e.g., routing)
    8.  Writing time series to files and databases
    9.  Checking time series
4.  Table processing commands:
    1.  Create tables
    2.  Read tables
    3.  Table/time series transfer
    4.  Manipulate tables
    5.  Analyze tables
    6.  Write tables
5.  Other data processing commands:
    1.  Datastores (databases)
    2.  Ensembles (groups of time series)
    3.  Network
    4.  Spatial data
    5.  Spreadsheet
    6.  Template
    7.  Visualization
6.  General commands:
    1.  Comments
    2.  File handling
    3.  Logging
    4.  Run control
    5.  Testing
7.  Built-in test framework, which is used to run functional tests, suitable for software developers and also
    non-programmers who want to validate processing workflows.
8.  Multiple run modes including batch, command shell interpreter, user interface, HTTP server.
9.  Integration with other tools to leverage the strengths of those tools.

## Repository Contents ##

The repository contains the following:

```text
.github/              Files specific to GitHub such as issue template.
.gitattributes        Typical Git configuration file for repository attributes.
.gitignore            Typical Git configuration file for ignored file list.
README.md             This file.
build-util/           Useful scripts to view, build, and deploy documentation.
mkdocs-project/       Typical MkDocs project for this documentation.
  mkdocs.yml          MkDocs configuration file for website.
  docs/               Folder containing source Markdown and other files for website.
    css/              Custom CSS to augment MkDocs theme.
  site/               Folder created by MkDocs containing the static website - ignored using .gitignore.

```

The repository can be cloned into the recommended standard CDSS development folder structure,
shown below.  Each of the component libraries have README files that indicate dependencies.

```text
C:\Users\user\                            Windows:  User's files.
/home/user/                               Linux:  User's files.
/cygdrive/C/Users/user/                   Cygwin:  User's files.
  cdss-dev/                               Main development location for CDSS products.
    TSTool/                               TSTool software development files.
      git-repos/                          Git repositories for TSTool software.
        cdss-app-tstool-doc/              Legacy user and developer documentation,
                                          primarily in Word/PDF.
        cdss-app-tstool-doc-dev/          Developer documentation using Markdown/MkDocs.
        cdss-app-tstool-doc-user/         User documentation using Markdown/MkDocs.
        cdss-app-tstool-main/             Main TSTool application, primarily the main UI.
        cdss-app-tstool-test/             Functional tests that run command files.
        cdss-lib-cdss-java/               Shared CDSS code.
        cdss-lib-common-java/             Shared general utility code.
        cdss-lib-dmi-hydrobase-java/      State of Colorado's HydroBase API.
        cdss-lib-dmi-nwsrfs-java/         Legacy National Weather Service API.
        cdss-lib-dmi-riversidedb-java/    Legacy RiversideDB database API.
        cdss-lib-dmi-satmonsys-java/      Colorado Satellite Monitoring System API.
        cdss-lib-models-java/             CDSS StateCU and StateMod model API.
        cdss-lib-processor-ts-java/       Core TSTool processing library.
        cdss-util-buildtools/             Utilities to build and deploy TSTool.
```

## Development Environment ##

The development environment for contributing to this documentation requires
installation of Python, MkDocs, and Material MkDocs theme.
Python 3 and MkDocs 1+ is currently used for development.
See the [OWF / Learn MkDocs](https://learn.openwaterfoundation.org/owf-learn-mkdocs/)
documentation for information about installing these tools.

## Editing and Viewing Content ##

If the development environment is properly configured, edit and view content as follows:

1.  Edit content in the `mkdocs-project/docs` folder and update `mkdocs-project/mkdocs.yml` as appropriate.
2.  Run the `build-util/run-mkdocs-serve-8000.sh` script (Cygwin/Linux) or equivalent.
3.  View content in a web browser using URL `http://localhost:8000`.

## Style Guide ##

The following are general style guide recommendations for this documentation,
with the goal of keeping formatting simple in favor of focusing on useful content:

*   Use the Material MkDocs theme - it looks nice, provides good navigation features, and enables search.
*   Follow MkDocs Markdown standards - use extensions beyond basic Markdown when useful.
*   Show files and program names as `code (tick-surrounded)` formatting.
*   Where a source file can be linked to in GitHub, provide a link so that the most current file can be viewed.
*   Use triple-tick formatting for code blocks, with language specifier.
*   Use ***bold italics*** when referencing UI components such as menus.
*   Use slashes to indicate ***Menu / SubMenu***.
*   Images are handled as follows:
    +   Where narrative content pages are sufficiently separated into folders,
        image files exist in those folder with names that match the original TSTool Word documentation.
        This approach has been used for the most part.
    +   If necessary, place images in a folder with the same name as the content file and include
        `-images` at the end of the folder name at the same level (for example `x.md` and `x-images/`)
        or include an `images` folder under the content folder.
    +   When using images in the documents, consider providing a link to look at the full-sized
        image, as follows (normal MkDocs approach does not seem to work?):

```text
The following figure illustrates the ***Mixed Station Analysis*** tool.
<a href="../Menu_Tools_Analysis_MixedStationAnalysis.png">See also the full-size image.</a>

![Mixed station analysis tools menu](Menu_Tools_Analysis_MixedStationAnalysis.png)
```
*   Minimize the use of inlined HTML elements, but use it where Markdown formatting is limited.
*   Although the Material them provides site and page navigation sidebars,
    provide in-line table of contents on pages, where appropriate, to facilitate review of page content.
    Use a simple list with links to sections on the page.

### Web Accessibility ###

Ensuring web accessibility for people with disabilities such as visual impairments is important.
See the following resources:

*   [Federal government:  Guidance on Web Accessibility and the ADA](https://www.ada.gov/resources/web-guidance/)
*   [State of Colorado:  Accessibility for Developers](https://oit.colorado.gov/standards-policies-guides/guide-to-accessible-web-services/accessibility-for-developers)

Specific guidance for this documentation includes:

*   Links:
    +   The MkDocs material custom CSS uses underlines for links to provide a visual cue because
        default reliance on color only is insufficient.
*   Image "alt text":
    +   "alt text" should be specified for all images using human-readable text to facilitate reading by audio tools.
    +   Because this is technical documentation,
        there is no way to fully avoid technical terms such as command names,
        but try to make the text generally understandable.
    +   Many images also have captions and the language for "alt text" may be similar to the caption.
    +   It is OK to include punctuation in "alt text".

## License ##

The license for this documentation is the
[Creative Commons Attribution International 4.0 (CC BY 4.0) license](https://creativecommons.org/licenses/by/4.0/).

## Contributing ##

Contribute to the documentation as follows:

1.  Use GitHub repository issues to report minor issues.
    Fill out the template issue.
2.  Use GitHub pull requests.
3.  A member of the core development team will follow up to issues and pull requests.

## Maintainers ##

This repository is maintained by the OpenCDSS team.

## Release Notes ##

The following release notes indicate the update major history for documentation.
See the GitHub issues and repository history for detailed information.

*   2023-08-07 - Update for 14.9.0 release (OpenJDK Java).
*   2023-03-27 - Update for 14.7.0 release (web accessibility).
*   2021-09-14 - Update for 14.0.0 release.
*   2019-04-26 - Update links for opencdss.state.co.us domain.
*   2019-01-04 - Update for public release on OpenCDSS.
*   2018-09-14 - Clean up documentation for TSTool 12.06.00 release.
*   2018-04-22 - Initial content migrated from other forms.
