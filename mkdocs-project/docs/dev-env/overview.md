# TSTool / Development Environment / Overview ##

This Development Environment documentation is intended to be used as a reference by the developer that
sets up the project for the first time or initializes a new development environment to contribute to the project.
Specific sections are referenced by the [Initial Project Setup](../project-init/overview/),
[Deployed Environment](../deployed-env/overview/), and
[New Developer](../dev-new/overview/) sections.

This documentation includes the following sections:

* [Development Environment Software Requirements](#development-environment-software-requirements)
* [Software Install Location Considerations](#software-install-location-considerations)
* [Portability Considerations](#portability-considerations)

-----

## Development Environment Software Requirements ##

The following software are needed in the TSTool development environment and should be installed before doing [Initial Project Setup](../project-init/overview/),
although the Initial Project Setup documentation generally indicates prerequisites for software that needs to be installed.
Steps can be skipped if they have been completed previously as part of operating system setup or on other software development projects.
Some additional software may be installed in the development files and is described in project initialization.

The development environment as described provides a full technology stack for development.
Software developers need to invest in training to be competent with the various tools,
although this documentation is intended to help facilitate development by providing useful information.

The following software are required for TSTool development:

1. [Machine](machine) - Windows 7/10 computer or Linux
2. [Git](git) - needed to perform command line version control operations
3. [Python and pip](python) - needed by MkDocs, and useful general tool (**skip if not editing MkDocs documentation**)
4. [MkDocs](mkdocs) - MkDocs is used for developer and user documentation static websites, including this documentation (**skip if not editing MkDocs documentation**)
5. [Java 8](java8) - used to run Eclipse, and can be used to write utility programs
6. [Eclipse](eclipse) - IDE used for interactive Java software development
7. [KDiff3](kdiff3) - tool for comparing files (**skip if not comparing files or have equivalent tool**)
8. [NSIS](nsis) - tool used to create software installer

## Software Install Location Considerations ##

The software development environment must be appropriately configured to effectively develop TSTool and support collaboration.
Development environment setup must occur before any code can be written
and is typically done the first time by someone that has a good grasp of the technologies.
Failing to understand how to set up the development environment will likely lead to wasted time
and possibly back-tracking on previous software development work.
Using a consistent development environment for all developers ensures that documentation is applicable and troubleshooting is consistent.
Therefore, the software installation locations described in this documentation are recommended to avoid issues.

See the discussion of [Initial Project Setup / Development Files Structure](../project-init/overview#development-files-structure)
for a folder structure that is assumed in this documentation.
It is important for software developers to understand the software tools and configuration so that they can troubleshoot configuration issues.

## Portability Considerations ##

The TSTool development environment is intended to be as portable as possible,
in order to allow multiple software developers to contribute to the software on multiple operating systems.
Portable configuration minimizes day-to-day conflicts in developer environment that result in lost productivity and software quality.
Portability considerations are discussed where appropriate.
For example, the Git repositories use `.gitattributes` file to ensure proper handling of end of line characters.
