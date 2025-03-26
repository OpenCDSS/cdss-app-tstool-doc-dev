# CDSS / TSTool (Developer) #

This developer documentation explains how to build, enhance, and maintain
[Colorado's Decision Support Systems (CDSS)](https://cdss.colorado.gov) TSTool software.
TSTool software automates processing time series, data tables, and other data.
See also the latest [TSTool User Documentation](https://opencdss.state.co.us/tstool/latest/doc-user/)
and the [OpenCDSS TSTool](https://opencdss.state.co.us/opencdss/tstool/) product documentation.

*   [How to Use this Documentation](#how-to-use-this-documentation)
*   [Acknowledgements](#acknowledgements)
*   [Colorado's Decision Support Systems](#colorados-decision-support-systems)
*   [About the Open Water Foundation](#about-the-open-water-foundation)
*   [License](#license)
*   [Source Repository on GitHub](#source-repository-on-github)
*   [Release Notes](#release-notes) - **this documentation has been updated for TSTool version 15.0.0**

----------------

## How to Use this Documentation ##

This website is a companion to the TSTool source code and provides guidance for software developers that modify and support TSTool.

The documentation is organized with the first sections focusing on setup for a new developer and common development tasks.
The reference sections at the end provide information that may be of use but are typically not used day to day.
Use the search feature of this website to find specific information.

As of TSTool version 14.8.7, OpenJDK Java is used.
Prior to this version, Oracle Standard Edition Java was used.
Refer to the [Development Environment / Java](dev-env/java/java.md) documentation for a list of TSTool and Java versions.

As of TSTool version 14.0.0, the TSTool development environment creates a 64-bit Java TSTool runtime for use on Windows and Linux computers,
using Oracle Standard Edition.
Older versions used the 32-bit Java runtime.

Icons for Cygwin ![Cygwin icon](images/cygwin-32.png), Linux ![Linux icon](images/linux-32.png), and Windows ![Windows icon](images/windows-32.png)
are included to help indicate documentation
specific to an operating system.

*   [New Developer Setup](dev-new/overview.md) - **new TSTool software developers should start here**
*   [Development Tasks](dev-tasks/overview.md) - describes common development tasks - **refer to this after a new development environment has been configured**
*   [REFERENCE: Software Design](software-design/overview.md) - provides details about the software code design
*   [REFERENCE: Deployed Environment](deployed-env/overview.md) - describes the deployed environment after software is installed
*   [REFERENCE: Development Environment](dev-env/overview.md) - describes development environment software installation
*   [REFERENCE: Initial Project Setup](project-init/overview.md) - describes initial project setup and file structure

Use the navigation menu provided on the left side of the page to navigate the documentation sections within the full document.
Use the navigation menu provided on the right side of the page to navigate the documentation sections with a page.
The navigation menus may not be displayed if the web browser window is narrow or if viewing on a mobile device,
in which case look for a menu icon to access the menus.
Use the search feature to find documentation matching the search words.

## Acknowledgements ##

TSTool has been developed by the Open Water Foundation (OWF) with significant
funding provided by the Colorado Water Conservation Board (CWCB)
in coordination with the Division of Water Resources (DWR),
as part of Colorado’s Decision Support Systems (CDSS).

Additional enhancements to TSTool have been funded by various organizations including:

*   Open Water Foundation
*   US Bureau of Reclamation
*   Tennessee Valley Authority
*   and others

TSTool software developers are encouraged to provide feedback using the
[GitHub Issues page](https://github.com/OpenCDSS/cdss-app-tstool-main/issues)
for the TSTool main application repository,
or the issues for the appropriate repositories.

Feedback specific to CDSS functionality (e.g.,
HydroBase, StateMod, StateModB, StateCU input)
can be provided using the [CDSS email address](mailto:DNR_OpenCDSS@state.co.us).

### Software Components ###

The following components are used in TSTool and require or request attribution:

*   [Material Theme icons](https://material.io/icons/) - these icons are used in documentation

## Colorado's Decision Support Systems ##

Colorado's Decision Support Systems (CDSS, [https://cdss.colorado.gov/](https://cdss.colorado.gov/))
has been developed to answer important questions about Colorado's water resources.
CDSS efforts are led by the [Colorado Water Conservation Board (CWCB)](https://cwcb.colorado.gov/)
and [Colorado Division of Water Resources (DWR)](https://dwr.colorado.gov/).

**<p style="text-align: center;">
![CDSS Website](index-images/CDSS-website.png)
</p>**

CDSS has been under development since 1994, with progress occurring via a series of basin
decision support systems (DSS), starting with the Colorado River DSS (CRDSS).
Other focused DSS were also developed, such as the CWCB's Instream Flow DSS.
Each DSS resulted in enhancements to the core CDSS tools,
which are envisioned as a general platform of data and tools to help with water supply planning.

The TSTool software was originally developed in CDSS to process time series and other data
from Colorado's HydroBase database into into water resources model data files.
Since the initial development, TSTool has been significantly enhanced to use additional data sources,
add commands with new functionality, and add new functionality to facilitate interactive
and automated data processing.

In late 2016, the Open Water Foundation began the effort to move TSTool and other CDSS software to open source licensing
and establish open source software projects, referred to as "OpenCDSS".
The OpenCDSS project has resulted in a significant evolution in how CDSS software development occurs,
such as implementing version control with Git/GitHub and modernizing the development environment and documentation.
See the [OpenCDSS Website](https://opencdss.state.co.us/opencdss/) for more information.

## About the Open Water Foundation ##

The [Open Water Foundation](https://openwaterfoundation.org) is a nonprofit social enterprise that focuses
on developing and supporting open source software for water resources,
so that organizations can make better decisions about water.
OWF also works to advance open data tools and implementation.
OWF staff have been the primary TSTool developers on State of Colorado and other projects.

## License ##

This TSTool documentation is licensed using the
[Creative Commons Attribution International 4.0 (CC BY 4.0) license](https://creativecommons.org/licenses/by/4.0/).

The TSTool software is licensed using the GPL 3 license (see the
[TSTool software repository](https://github.com/OpenCDSS/cdss-app-tstool-main)).

## Source Repository on GitHub ##

The source files for this documentation are maintained in a GitHub repository:
[cdss-app-tstool-doc-dev](https://github.com/OpenCDSS/cdss-app-tstool-doc-dev).

This developer documentation is currently maintained in a repository that is separate from TSTool code
in order to avoid confusion with the legacy documentation and to facilitate updates.

## Release Notes ##

See the [TSTool release notes](https://opencdss.state.co.us/tstool/latest/doc-user/appendix-release-notes/release-notes/)
section of the TSTool user documentation for information about TSTool software changes.
