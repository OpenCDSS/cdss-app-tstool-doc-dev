# TSTool / Development Environment / NSIS ##

Nullsoft Scriptable Install System (NSIS) software is used to create the Windows installer for TSTool.

* [NSIS Installation](#nsis-installation)
* [NSIS Add-ons](#nsis-add-ons)

----

## NSIS Installation ##

Install the appropriate version of the software for the operating system from the download page on the following page.

* [NSIS on SourceForge](https://sourceforge.net/projects/nsis/)

NSIS provide the benefit of being scriptable and therefore fits with automating creation of the installer.

NSIS version 2.46 is currently used and should be installed using [archived nsis-2.46-setup.exe installers](https://sourceforge.net/projects/nsis/files/NSIS%202/).
Accept all the defaults for the installation.
**The NSIS version needs to be updated to a later version to better handle Windows 10.**

## NSIS Add-ons ##

The core NSIS software does not provide all the necessary functionality.
Additional NSIS components were apparently installed on the main software,
but it is unclear where to retrieve such files that are compatible with NSIS 2.46.
Therefore, the following repository has been created with NSIS 2.46 files from an older computer used to create TSTool installers:

* [cdss-archive-nsis-2.46](https://github.com/OpenWaterFoundation/cdss-archive-nsis-2.46)

The following files in particular were copied into the `C:\Program Files (x86)\NSIS` to get the TSTool install process working
(clone the above repository and then copy files as needed):

* Contrib/
	+ `Graphics/`
		- `UltraModernUI/`
	+ `InstallOptiohnsEx/`
	+ `NSISArray/`
	+ `SetCursor/`
	+ `SkinnedControls/`
	+ `UltraModernUI/`
	+ `UIs/`
		- `UltraModernUI/`
		- `default_sb.exe`
		- `modern_sb.exe`
* Include/
	+ `MUIEx.nsh`
	+ `NSISArray.nsh`
	+ `Registry.nsh`
	+ `TextReplace.nsh`
	+ `UMUI.nsh`
* Plugins/
	+ `InstallOptionsEx.dll`
	+ `InstallOptionsEx_legacy.dll`
	+ `InstallOptionsEx_newAPI.dll`
	+ `NSISArray.dll`
	+ `NSISArray_legacy.dll`
	+ `NSISArray_newAPI.dll`
	+ `Registry.dll`
	+ `SetCursor.dll`
	+ `SkinnedControls.dll`
	+ `TextReplace.dll`
