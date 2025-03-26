# TSTool / Resources #

The following are useful resources.

*   [Ant](#ant) - software to control build processes in development environment
*   [Cygwin](#cygwin) - Linux-like environment for Windows
*   [Eclipse](#eclipse) - integrated development environment software
*   [Java](#java) - Java environment is used for development and runtime
*   [Jython](#jython) - Java implementation of Python
*   [KDiff3](#kdiff3) - visual difference tool
*   [Launch4J](#launch4j) - software to launch TSTool at runtime
*   [MkDocs](#mkdocs) - software used to create documentation
*   [Markdown](#markdown) - markup language for documentation
*   [Maven](#maven) - software to control build processes in development environment
*   [NSIS](#nsis) - used to create Windows software installer
*   [SLF4J](#slf4j) - standard logging framework

--------------------

## Ant ##

Ant is the build automation tool used by Eclipse.
It is currently used by the TSTool build utilities.
The newer [Maven](#maven) software is often now used instead of Ant but is not currently used for TSTool.

*   [Ant](https://ant.apache.org/)

## Cygwin ##

Cygwin is a Linux-like environment that runs on Windows.
It is an alternative to Git Bash that is included with Git for Windows.
Cygwin does introduce some issues.
For example, text file line endings in Git repositories can get mixed up when
switching between Git Bash and Cygwin terminal.
The file execute permissions can also be odd when switching between Git Bash and Windows.
Therefore, it is recommend that Cygwin only be used when Git Bash is not used.

*   [Cygwin](https://www.cygwin.com/)

## Eclipse ##

Eclipse is a popular open source integrated development environment (IDE) and has
historically been used for TSTool development.
The standard Java version is adequate (no need for EE version).

*   [Eclipse](https://www.eclipse.org/ide/)

## Java ##

Java is the underlying language an environment used by TSTool.

*   [Java](https://www.oracle.com/java/index.html)

## Jython ##

Jython provides a Java implementation of Python, which allows Python to be integrated with TSTool.
A major issue with Jython is whether Python 3 integration will be supported.

*   [Jython](https://www.jython.org/)

## KDiff3 ##

KDiff3 software is useful for visually comparing individual files and folders of files.

*   [KDiff3](https://kdiff3.sourceforge.net/)

## Launch4J ##

Launch4J is used to launch TSTool at runtime and provides control over the JRE.
It is used in the build utilities.

*   [Launch4J](https://launch4j.sourceforge.net/)

## MkDocs ##

Markdown is used to create this documentation. See also the [Markdown](#markdown) section below.

*   [MkDocs](https://www.mkdocs.org/) - MkDocs website
*   [OWF / Learn MkDocs](https://learn.openwaterfoundation.org/owf-learn-mkdocs/) - Open Water Foundation MkDocs learning resources

## Markdown ##

Markdown is used to create this documentation.
Markdown files, for example named `README.md`, can be also be created in TSTool working files to
document data processing workflows.

*   [Markdown on Wikipedia](https://en.wikipedia.org/wiki/Markdown)
*   [Mastering Markdown on GitHub](https://guides.github.com/features/mastering-markdown/)
*   [Adam Pritchard's Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
*   [GitHub Markdown language support](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml) - use to format code blocks

## Maven ##

Maven software provides tools to handle software library dependencies and automate software development tasks.
Maven often replaces Ant as a newer generation of build tools.
Maven has not yet been adopted for TSTool development but may be implemented in the future.

*   [Maven](https://maven.apache.org/)
*   [Maven Central](https://search.maven.org/)

## NSIS ##

NSIS is used to create Windows software installers via automated scripts.

*   [NSIS](https://sourceforge.net/projects/nsis/)

## SLF4J ##

SLF4J is a standard logging framework that allows logging messages from other frameworks
to be handled through a common interface.
SLF4J has not yet been integrated into TSTool - the legacy `Message` class is used instead.

*   [SLF4J](https://www.slf4j.org/)
