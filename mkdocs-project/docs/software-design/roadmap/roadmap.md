## Future Design Elements ##

Major enhancements that are envisioned are listed below, in no particular order.
This list is not comprehensive.
See the [TSTool repository issues](https://github.com/OpenCDSS/cdss-app-tstool-main/issues)
for a current list of issues.
Other related repositories also contain issues.
Some enhancements will require significant effort because features are used throughout the software.

1. Upgrade to use Java 9 and continue updating as new versions of Java are released.
	* Utilize new features.
	* Evaluate the module system to help with dependency management and plugins.
	* Move from Oracle Java to OpenJDK.
2. Resolve remaining 64-bit migration issues:
	* This mainly includes enabling the HEC-DSS features using 64-bit native libraries.
3. Enable robust plugin support to facilitate third-party component development.
4. Update development environment to use Maven for dependency management and automation.
5. Evaluate updating the development environment to NOT store Eclipse artifacts in repositories,
to support more development environments.
6. Split currently embedded packages into plugins for components that are maintained
by third parties (rather than core CDSS/TSTool team), potentially:
	* ReclamationHDB datastore
	* National Weather Service datastores
	* etc.
7. Migrate logging to SL4J logging framework.
8. Evaluate integration with Python/Jython and other languages.
9. General code cleanup of legacy code.
10. Add support for indentation in command files.
11. Evaluate migrating from Swing to JavaFX user interface framework.
