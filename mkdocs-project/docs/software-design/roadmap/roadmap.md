## Future Design Elements ##

Major enhancements that are envisioned are listed below, in no particular order.
This list is not comprehensive and additional items will be added as
legacy documentation is migrated to this developer manual and repository issues tracker.
Some enhancements will require significant effort because features are used throughout the software.

1. Upgrade to use Java 9.
	* Utilize new features.
	* Evaluate the module system to help with dependency management and plugins.
2. Update the development environment to support 32-bit and 64-bit runtimes
	* Focus is currently 32-bit because some components such as HEC-RAS API uses
	32-bit native libraries.
3. Enable robust plugin support to facilitate third-party component development.
4. Move to online documentation and phase out Word/PDF packaging in installer.
5. Update installer to use latest NSIS and Launch4J.
6. Update development environment to use Maven for dependency management and automation.
7. Update development environment to NOT store Eclipse artifacts in repositories,
to support more development environments.
8. Split currently embedded packages into plugins for components that are maintained
by third parties (rather than core CDSS/TSTool team), potentially:
	* ReclamationHDB datastore
	* RiversideDB datastore
	* National Weather Service datastores
9. Migrate logging to SL4J logging framework.
10. Evaluate integration with Python/Jython and other languages.
11. General code cleanup of legacy code.
12. Add support for indentation in command files.
13. Evaluate migrating from Swing to JavaFX user interface framework.
