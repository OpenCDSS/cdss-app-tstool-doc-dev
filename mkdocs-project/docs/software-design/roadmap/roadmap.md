# TSTool / Software Design / Development Roadmap #

TSTool maintenance and enhancement occurs based on available funding and necessity for project work.

Major enhancements that are envisioned are listed below, in no particular order.
This list is not comprehensive.
See the [TSTool repository issues](https://github.com/OpenCDSS/cdss-app-tstool-main/issues)
for a current list of issues.
Other related repositories also contain issues.
Some enhancements will require significant effort because features are used throughout the software.

1.  Upgrade to use Java 11, 17, and other long-term support (LTS) releases
    and continue updating as new versions of Java are released.
    *   Utilize new features.
    *   Evaluate the module system to help with dependency management and plugins.
2.  Enable robust plugin support to facilitate third-party component development:
    *   Standardize supporting library code.
    *   Enhance the plugin manager introduced in TSTool 15 to help with versions and dependency management.
3.  Update development environment to use Maven for dependency management and automation.
4.  Evaluate updating the development environment to NOT store Eclipse artifacts in repositories,
    to support more development environments.
5.  Split currently embedded packages into plugins for components that are maintained
    by third parties (rather than core CDSS/TSTool team), potentially:
    *   ReclamationHDB datastore
    *   National Weather Service datastores
    *   etc.
6.  Migrate logging to SL4J logging framework.
7.  Evaluate integration with Python/Jython and other languages.
8.  General code cleanup of legacy code.
9. Evaluate migrating from Swing to JavaFX user interface framework.
10. Update dependencies to latest versions and expose new functionality,
    for example for Excel integration.
