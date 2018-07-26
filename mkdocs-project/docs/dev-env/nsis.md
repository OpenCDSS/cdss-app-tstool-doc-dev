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

## NSIS Plug-Ins ##

The core NSIS software does not provide all the necessary functionality.
Additional NSIS components were apparently installed on the main software,
but it is unclear where to retrieve such files that are compatible with NSIS 2.46.
Therefore, the following repository has been created with NSIS 2.46 files from an older computer used to create TSTool installers:

* [cdss-archive-nsis-2.46](https://github.com/OpenWaterFoundation/cdss-archive-nsis-2.46)

The following files in particular were copied into the `C:\Program Files (x86)\NSIS` to get the TSTool install process working
(clone the above repository and then copy files as needed):

### `Contrib/` Folder: ###
| **Component for Plugin&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;** | Description | Where to Download | Comments |
| --- | --- | --- | --- |   
| `Graphics/UltraModernUI/` | Image files (`.bmp`) for modern installer look. | [UltraModernUI on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) | Part of the UltraModernUI plug-in. Causes no errors if not included in NSIS when building TSTool installer. The current installer doesn't utilize any of these Graphics, but without the folder you cannot use them in the future with NSIS.|  
| `InstallOptionsEx/`| This plugin is an extension for the original [InstallOptions](http://nsis.sourceforge.net/Docs/InstallOptions/Readme.html) plug-in you find with NSIS package. For those who want to have a more professional looking NSIS page. | [UltraModernUI on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or [InstallOptionsEX plug-in](http://nsis.sourceforge.net/InstallOptionsEx_plug-in) | Part of the InstallOptionsEx plug-in, but included in UltraModernUI plugin as well. Causes no errors if not included in NSIS when building TSTool installation. May offer beneficial features for the future, however. |
| `nsArray/` | A much simpler and smaller DLL than [NSISArray](http://nsis.sourceforge.net/Arrays_in_NSIS#NSISArray_plug-in_.28deprecated.29). Provides less out-of-the-box functionality but is faster and uses less memory. Supports any number of named dynamic arrays, indexed or hashed arrays, value getting, setting, insertion, removal, copying, joining and sorting (via quick sort algo.) | [UltraModernUI on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or [nsArray](http://nsis.sourceforge.net/Arrays_in_NSIS#nsArray_plug-in) | Part of the nsArray plug-in, but included in UltraModernUI. Before NSIS was using NSISArray which is deprecated and has been replaced with nsArray. Causes no errors if not included in NSIS when building TSTool installation. |
| `SetCursor/` | An NSIS plugin to set the cursor or change its position. | [SetCursor](http://nsis.sourceforge.net/SetCursor_plug-in) | SetCursor is it's own plug-in, separate from UltraModernUI. Causes no errors if not included in NSIS when building TSTool installation. | 
| `SkinnedControls/` | This NSIS plug-in allows to skin all buttons and scroll bars of your installer and allows to select text colors on buttons even those on custom pages. | [UltraModernUI on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or  [SkinnedControlls](http://nsis.sourceforge.net/SkinnedControls_plug-in) | Part of the SkinnedControls plug-in, but included in UltraModernUI. |
| `UIs/UltraModernUI/` </br> `UIs/default_sb.exe` </br> `UIs/modern_sb.exe` | UI's for UltraModernUI | [UltraModernUI on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) | Part of the UltraModernUI plug-in. If not included in NSIS there will be errors with building the TSTool Installer. |
| `UltraModernUI/` | The main UltraModernUI | [UltraModernUI on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) | This is the main component for UltraModernUI and is absolutely necessary for using the UltraModernUI plug-in. If not included in NSIS there will be errors with building the TSTool installer. |

**Necessary files for `Contrib/` Folder**:
* `Contrib/UIs/UltraModernUI`
* `Contrib/UIs/default_sb.exe`
* `Contrib/UIs/modern_sb.exe`
* `Contrib/UltraModernUI`


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
