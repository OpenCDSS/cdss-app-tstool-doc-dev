# TSTool / Development Environment / NSIS ##

Nullsoft Scriptable Install System (NSIS) software is used to create the Windows
installer for TSTool.

* [NSIS Installation](#nsis-installation)
* [NSIS Add-ons for NSIS 3.03](#nsis-add-ons-for-nsis-303)
    * [Contrib Folder](#contrib-folder)
	  * [Include Folder](#include-folder)
	  * [Plugins Folder](#plugins-folder)
* [NSIS Add-ons for NSIS 2.46](#nsis-add-ons-for-nsis-246)

----

## NSIS Installation ##

Install version 3.03 of the software for the development version operating system
from the download page on the following page.

* [NSIS on SourceForge](https://sourceforge.net/projects/nsis/)

NSIS provides the benefit of being scriptable and therefore fits with automating
creation of the installer.

## NSIS Add-ons for NSIS 3.03 ##

The core NSIS software does not provide all the necessary functionality.
Additional NSIS components were apparently installed in the main software location.

The following files were copied into the `C:\Program Files (x86)\NSIS`
necessary for the TSTool install process. Files from original sources are used and where notes files are copied from the [NSIS 2.46 archive repository](https://github.com/OpenWaterFoundation/cdss-archive-nsis-2.46)

The following files were added many years ago and it is not clear what files are
still needed in the NSIS program files for the TSTool installer to build properly.
In the comments section of each file there is mention of whether or not TSTool
installer was still able to get built with or without the file present in the NSIS
program files.

Files in bold and listed below each table are necessary and would
result in build errors if not included. Files not bolded may be phased out over
time, but are being kept as to not cause any potential issues if they are actually
needed, but this was not apparent in testing.

### `Contrib/` Folder: ###
| **Component for Plugin&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;** | Description | Where to Download | Comments |
| --- | --- | --- | --- |   
| `Graphics/UltraModernUI/` | Image files (`.bmp`) for modern installer look. | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) | Part of the UltraModernUI 2.0 beta 4 plug-in. Causes no errors if not included in NSIS when building TSTool installer. The current installer doesn't utilize any of these Graphics, but without the folder you cannot use them in the future with NSIS.|  
| `InstallOptionsEx/`| This plugin is an extension for the original [InstallOptions](http://nsis.sourceforge.net/Docs/InstallOptions/Readme.html) plug-in distributed with NSIS, for those who want to have a more professional looking NSIS page. | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or [InstallOptionsEX 2.4.5 plug-in](http://nsis.sourceforge.net/InstallOptionsEx_plug-in) | Part of the InstallOptionsEx plug-in, but included in UltraModernUI plugin as well. Causes no errors if not included in NSIS when building TSTool installation. May offer beneficial features for the future, however. |
| `nsArray/` | A much simpler and smaller DLL than [NSISArray](http://nsis.sourceforge.net/Arrays_in_NSIS#NSISArray_plug-in_.28deprecated.29). Provides less out-of-the-box functionality but is faster and uses less memory. Supports any number of named dynamic arrays, indexed or hashed arrays, value getting, setting, insertion, removal, copying, joining and sorting (via quick sort algo.) | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or [nsArray](http://nsis.sourceforge.net/Arrays_in_NSIS#nsArray_plug-in) | Part of the nsArray plug-in, but included in UltraModernUI. Before NSIS was using NSISArray which is deprecated and has been replaced with nsArray. Causes no errors if not included in NSIS when building TSTool installation. |
| `SetCursor/` | An NSIS plugin to set the cursor or change its position. | [SetCursor](http://nsis.sourceforge.net/SetCursor_plug-in) | SetCursor is it's own plug-in, separate from UltraModernUI. Causes no errors if not included in NSIS when building TSTool installation. |
| `SkinnedControls/` | This NSIS plug-in allows using a "skin" for buttons and scroll bars of the installer and allows selecting text colors on buttons, even those on custom pages. Causes no errors if not included in NSIS when building TSTool installation. | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or  [SkinnedControls 1.4](http://nsis.sourceforge.net/SkinnedControls_plug-in) | Part of the SkinnedControls plug-in, but included in UltraModernUI. |
| **`UIs/UltraModernUI/`** </br> **`UIs/default_sb.exe`** </br> **`UIs/modern_sb.exe`** | UI's for UltraModernUI | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) | Part of the UltraModernUI plug-in. If not included in NSIS there will be errors with building the TSTool Installer. |
| **`UltraModernUI/`** | The main UltraModernUI | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) | This is the main component for UltraModernUI and is absolutely necessary for using the UltraModernUI plug-in. If not included in NSIS there will be errors with building the TSTool installer. |

**Necessary files for `Contrib/` Folder**:  
These are the essential files that must be included in the NSIS 3.03 `Contrib/` folder
to ensure that the TSTool installer will build properly with no errors.

* `Contrib/UIs/UltraModernUI`  
* `Contrib/UIs/default_sb.exe`  
* `Contrib/UIs/modern_sb.exe`  
* `Contrib/UltraModernUI`  

### `Include/` Folder: ###

| **Component for Plugin&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;** | Description | Where to Download | Comments |
| --- | --- | --- | --- |
| `MUIEx.nsh` | Includes `Contrib/UltraModernUI/UMUI.nsh` in NSIS build. | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) | Causes no errors if not included in NSIS when building TSTool installation. |
| `nsArray.nsh` | Includes necessary information for `Contrib/nsArray/` | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or [nsArray](http://nsis.sourceforge.net/Arrays_in_NSIS#nsArray_plug-in) | Causes no errors if not included in NSIS when building TSTool installer. |
| **`Registry.nsh`** | Includes necessary information for `Plugins/Registry.dll` | [Registry 4.1](http://nsis.sourceforge.net/Registry_plug-in) | If not included in NSIS there will be errors with building the TSTool installer. |
| **`TextReplace.nsh`** | Includes necessary information for `Contrib/TextReplace.dll` | [TextReplace 1.5](http://nsis.sourceforge.net/TextReplace_plugin) | If not included in NSIS there will be errors with building the TSTool installer. |
| **`UMUI.nsh`** | Appears to also include `Contrib/UltraModernUI/UMUI.nsh`. Not sure the difference between this file and `MUIEx.nsh` |  [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) | If not included in NSIS there will be errors with building the TSTool installer. |

**Necessary files for `Include/` Folder**:  
These are the essential files that must be included in the NISI program `Include/`
folder to ensure that TSTool installer will build properly with no errors.

* `Include/Registry.nsh`
* `Include/TextReplace.nsh`
* `Include/UMUI.nsh`

### `Plugins/` Folder: ###
NSIS 2.46 strictly used `x86-ansi` for `.dll` files. NSIS 3.03 has updated to
include both `x86-ansi` and `x86-unicode` for `.dll` files. If adding a plug-in
that only includes one `.dll` file, it is safe to assume this will be `x86-ansi`.

| **Component for Plugin&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;** | Description | Where to Download | Comments |
| --- | --- | --- | --- |
| `InstallOptionsEx.dll` |  Dynamic link library for InstallOptionsEx plug-in. This plugin is an extension for the original [InstallOptions](http://nsis.sourceforge.net/Docs/InstallOptions/Readme.html) plug-in distributed with NSIS, for those who want to have a more professional looking NSIS page. | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or [InstallOptionsEX 2.4.5 plug-in](http://nsis.sourceforge.net/InstallOptionsEx_plug-in) | Causes no errors if not included in NSIS when building TSTool. |
| `nsArray.dll` | Dynamic link library for nsArray plug-in. Before NSIS was using NSISArray which is deprecated and has been replaced with nsArray. Causes no errors if not included in NSIS when building TSTool installation. | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or [nsArray](http://nsis.sourceforge.net/Arrays_in_NSIS#nsArray_plug-in) | Causes no errors if not included in NSIS when building TSTool installer. |
| `Registry.dll` | Dynamic link library for Registry plug-in. This is NSIS plug-in for registry. Archive also contains PPC-Registry plugin for Pocket PC. | [Registry 4.1](http://nsis.sourceforge.net/Registry_plug-in) | Causes no errors if not included in NSIS when building TSTool installer. |
| **`SetCursor.dll`** | Dynamic link library for SetCursor plug-in. An NSIS plugin to set the cursor or change its position. | [SetCursor](http://nsis.sourceforge.net/SetCursor_plug-in) | If not included in NSIS there will be errors with building the TSTool installer. |
| **`SkinnedControls.dll`** | Dynamic link library for SkinnedControl plug-in. This NSIS plug-in allows using a "skin" for buttons and scroll bars of the installer and allows selecting text colors on buttons, even those on custom pages. Causes no errors if not included in NSIS when building TSTool installation. | [UltraModernUI 2.0 beta 4 on GitHub](https://github.com/SuperPat45/UltraModernUI/releases) or  [SkinnedControls 1.4](http://nsis.sourceforge.net/SkinnedControls_plug-in) | If not included in NSIS there will be errors when building the TSTool installer. |
| **`TextReplace.dll`** | Dynamic link library for TextReplace plug-in. | [TextReplace 1.5](http://nsis.sourceforge.net/TextReplace_plugin) | If not included in NSIS there will be errors when building the TSTool installer. |

**Necessary file for `Plugins/` Folder**:

 * `Plugins/SetCursor.dll`
 * `Plugins/SkinnedControls.dll`
 * `Plugins/TextReplace.dll`

## NSIS Add-ons for NSIS 2.46 ##

*This section is retained as a historical reference for use withy TSTool 12.05.00 and earlier.*

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
