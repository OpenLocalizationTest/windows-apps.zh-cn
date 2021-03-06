---
author: awkoren
Description: Run the Desktop Converter App to convert a Windows desktop application (like Win32, WPF, and Windows Forms) to a Universal Windows Platform (UWP) app.
Search.Product: eADQiWindows 10XVcnh
title: Desktop App Converter Preview (Project Centennial)
---

# Desktop App Converter Preview (Project Centennial)

\[Some information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.\]

[Get the Desktop App Converter.](http://go.microsoft.com/fwlink/?LinkId=785437)

Desktop App Converter is a pre-release tool that enables you to bring your existing desktop apps written for .NET 4.6.1 or Win32 to the Universal Windows Platform (UWP). You can run your desktop installers through the converter in an unattended (silent) mode and obtain an AppX package that you can install by using the Add-AppxPackage PowerShell cmdlet on your development machine.

The converter runs the desktop installer in an isolated Windows environment using a clean base image provided as part of the converter download. It captures any registry and file system I/O made by the desktop installer and packages it as part of the output. The converter outputs an AppX with package identity and the ability to call a vast range of WinRT APIs.

## What's new

This section outlines changes between versions of the Desktop App Converter. 

### 6/8/2016

* Added support for generating x86 appx packages on AMD64 host machines running the converter.
* Reduced disk space usage by removing any previously expanded base images.
* Added support for cleaning up temporary files and any unnecessary base images.
* Improved support for detecting file type and protocol associations.
* Improved logic to detect the AppExecutable property for a large set of apps.
* Added support for providing additional –InstallerArguments for MSI based installers.
* Bug fixes for any PathTooLongException errors during the conversion process.

### 5/12/2016

- Restored support for Pro edition of Windows. 
- Converter ```-Setup``` flag now enables Windows Containers feature and handles base image expansion. Run the following from an elevated PowerShell prompt to do one time setup: ```PS C:\> .\DesktopAppConverter.ps1 -Setup -BaseImage BaseImage-12345.wim -Verbose```
- Added auto-detection of app install path and moving application root outside of VFS to reduce any unnecessary file system redirections at runtime.
- Added auto-detection of the expanded base image as part of the conversion process.
- Added auto-detection for file type associations and protocols.
- Improved logic to detect Start Menu shortcut.
- Improved file system filtering to retain app installed MUI files.
- Updated the minimum supported desktop version (10.0.14342.0) for Project Centennial in the manifest.

## System requirements

### Supported operating system
+ Windows 10 Anniversary Update Enterprise edition preview (Build 10.0.14342.0 and later)

### Required hardware configuration

Your computer must have the following minimum capabilities:
+ 64 bit (x64) processor
+ Hardware-assisted virtualization
+ Second Level Address Translation (SLAT)

### Recommended resources
+ [Windows Software Development Kit (SDK) for Windows 10](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk)

## Set up the Desktop App Converter   
Desktop App Converter relies on Windows 10 features that are flighted as part of the Windows Insider Preview builds. Make sure that you're on the latest build to utilize the converter.

1. Ensure that you have the latest Windows 10 Insider Preview OS – Enterprise or Pro edition (http://insider.windows.com). 
2. Download the DesktopAppConverter.zip and the base image .wim file that matches your Insider Preview build (http://aka.ms/converter). 
3. Extract the DesktopAppConverter.zip to a local folder.
4. From an admin PowerShell window:  
```CMD
PS C:\> Set-ExecutionPolicy bypass
```
5. Run the following command from an admin PowerShell window to setup the converter:
```CMD
PS C:\> .\DesktopAppConverter.ps1 -Setup -BaseImage .\BaseImage-1XXXX.wim -Verbose
```
6. If running the previous command prompts you to reboot, restart your machine and run the command again.

## Run the Desktop App Converter
Desktop App Converter has two entry points: PowerShell and Command Shell. You can use either of these entry points to start the conversion process.

### Usage
```CMD
DesktopAppConverter.ps1
-Installer <String> [-InstallerArguments <String>] [-InstallerValidExitCodes <Int32>]
-Destination <String>
-PackageName <String>
-Publisher <String>
-Version <Version>
[-ExpandedBaseImage <String>]
[-AppExecutable <String>]
[-AppFileTypes <String>]
[-AppId <String>]
[-AppDisplayName <String>]
[-AppDescription <String>]
[-PackageDisplayName <String>]
[-PackagePublisherDisplayName <String>]
[-MakeAppx]
[-LogFile <String>]
[<CommonParameters>]  
```

### Example
The following example shows how to convert a desktop app named *MyApp* by *&lt;publisher_name&gt;* to a UWP package (AppX).

+ From an admin PowerShell window, run the following command:
```CMD
PS C:\>.\DesktopAppConverter.ps1 -Installer C:\Installer\MyApp.exe 
-InstallerArguments "/S" -Destination C:\Output\MyApp -PackageName "MyApp" 
-Publisher "CN=<publisher_name>" -Version 0.0.0.1 -MakeAppx -Verbose
```

## Deploy your converted AppX
Use the [Add-AppxPackage](https://technet.microsoft.com/en-us/library/hh856048.aspx) cmdlet in PowerShell to deploy a signed app package (.appx) to a user account. To sign your .appx package, refer to the following section, "Signing your .Appx Package". Also, you can include the *Register* parameter of the cmdlet to install from a folder of unpackaged files during the development process. For more info, see [Deploy and debug your converted UWP app](desktop-to-uwp-deploy-and-debug.md).

## Sign your .Appx Package

The Add-AppxPackage cmdlet requires that the application package (.appx) being deployed must be signed. Use SignTool.exe, which ships in the Microsoft Windows 10 SDK, to sign the .appx package.

### Example
```CMD
C:\> MakeCert.exe -r -h 0 -n "CN=<publisher_name>" -eku 1.3.6.1.5.5.7.3.3 -pe -sv <my.pvk> <my.cer>
C:\> pvk2pfx.exe -pvk <my.pvk> -spc <my.cer> -pfx <my.pfx>
C:\> signtool.exe sign -f <my.pfx> -fd SHA256 -v .\<outputAppX>.appx
```
**Note:** When you run MakeCert.exe and you're asked to enter a password, select **None**.

For more info on certificates and signing, see:

+ [How to: Create Temporary Certificates for Use During Development](https://msdn.microsoft.com/library/ms733813.aspx)
+ [SignTool](https://msdn.microsoft.com/library/windows/desktop/aa387764.aspx)
+ [SignTool.exe (Sign Tool)](https://msdn.microsoft.com/library/8s9b9yaz.aspx)

### Caveats
1. The Windows 10 build on the host machine must match the base image that you obtained as part of the Desktop App Converter download.  
2. Ensure that the desktop installer is in an independent directory, because the converter copies all of the directory's content to the isolated Windows environment.  
3. Currently, the Desktop App Converter supports running the conversion process on a 64-bit operating system only. You can deploy the converted .appx packages to a 64-bit (x64) OS only.  
4. Desktop App Converter requires the desktop installer to run under unattended mode. Ensure that you pass the silent flag for your installer to the converter by using the *-InstallerArguments* parameter.
5. Publishing public SxS Fusion assemblies won't work. During install, an application can publish public side-by-side Fusion assemblies, accessible to any other process. During process activation context creation, these assemblies are retrieved by a system process named CSRSS.exe. When this is done for a Centennial process, activation context creation and module loading of these assemblies will fail. Inbox assemblies, like ComCtl, are shipped with the OS, so taking a dependency on them from Centennial processes is safe. The SxS Fusion assemblies are registered in the following locations:
  + Registry: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\SideBySide\Winners`
  + File System: %windir%\\SideBySide

## Known issues

+ If you receive a Windows Insider flight on a developer machine that previously had the Desktop App Converter Preview installed, you may receive the error `New-ContainerNetwork: The object already exists` when you setup the new base image. As a workaround, run the command `Netsh int ipv4 reset` from an elevated command prompt, then reboot your machine. 
+ A .NET app compiled with "AnyCPU" build option will fail to install if the main executable or any of the dependencies were placed under "Program Files" or "Windows\System32". As a workaround, please use your architecture specific desktop installer (32 bit or 64 bit) to successfully generate an AppX package.

## Telemetry from Desktop App Converter  
Desktop App Converter may collect information about you and your use of the software and send this info to Microsoft. You can learn more about Microsoft's data collection and use in the product documentation and in the [Microsoft Privacy Statement](http://go.microsoft.com/fwlink/?LinkId=521839). You agree to comply with all applicable provisions of the Microsoft Privacy Statement.

By default, telemetry will be enabled for the Desktop App Converter. Add the following registry key to configure telemetry to a desired setting:  
```CMD
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DesktopAppConverter
```
+ Add or edit the *DisableTelemetry* value by using a DWORD set to 1.
+ To enable telemetry, remove the key or set the value to 0.

## Desktop App Converter usage
Here's a list of parameters to the Desktop App Converter. You can also view this list in the Windows Powershell window by running the following command:  
```CMD
get-help .\DesktopAppConverter.ps1 -detailed
```

### Setup Parameters  
|Parameter|Description|
|---------|-----------|
|```-Setup [<SwitchParameter>]``` | Runs DesktopAppConverter in setup mode. Setup mode supports expanding a provided base image.|
|```-BaseImage <String>``` | Full path to an unexpanded base image. This parameter is required if -Setup is specified.|
|```-LogFile <String>``` [optional] | Specifies a log file. If omitted, a log file temporary location will be created.|
|```-NatSubnetPrefix <String>``` [optional] | Prefix value to be used for the Nat instance. Typically, you would want to change this only if your host machine is attached to the same subnet range as the converter's NetNat. You can query the current converter NetNat config by using the **Get-NetNat** cmdlet. |
|```-NoRestart [<SwitchParameter>]``` | Don't prompt for reboot when running setup (reboot is required to enable the container feature). |

### Conversion Parameters  
|Parameter|Description|
|---------|-----------|
|```-Installer <String>``` | The path to the installer for your application - must be able to run unattended/silently|
|```-InstallerArguments <String>``` [optional] | A comma-separated list or string of arguments to force your installer to run unattended/silently. This parameter is optional if your installer is an msi. To get a log from your installer, supply the logging argument for the installer here and use the path ```<log_folder>```, which is a token that the converter replaces with the appropriate path. <br><br>**NOTE: The unattended/silent flags and log arguments will vary between installer technologies.** <br><br>An example usage for this parameter: ```-InstallerArguments "/silent /log <log_folder>\install.log"``` Another example that doesn't produce a log file may look like: ```-InstallerArguments "/quiet", "/norestart"``` Again, you must literally direct any logs to the token path ```<log_folder>``` if you want the converter to capture it and put it in the final log folder.|
|```-InstallerValidExitCodes <Int32>``` [optional] | A comma-separated list of exit codes that indicate your installer ran successfully (for example: 0, 1234, 5678).  By default this is 0 for non-msi, and 0, 1641, 3010 for msi.|
|```-Destination <String>``` | The desired destination for the converter's appx output - DesktopAppConverter can create this location if it doesn't already exist.|

### Appx Identity Parameters  
|Parameter|Description|
|---------|-----------|
|```-PackageName <String>``` | The name of your Universal Windows App package
|```-Publisher <String>``` | The publisher of your Universal Windows App package
|```-Version <Version>``` | The version number for your Universal Windows App package

### Optional Appx Manifest Parameters  
|Parameter|Description|
|---------|-----------|
|```-AppExecutable <String>``` [optional] | The full path to your application's main executable if it were to be installed (it doesn't have to be), for example, "C:\Program Files (x86)\MyApp\MyApp.exe".|
|```-AppFileTypes <String>``` [optional] | A comma-separated list of file types which the application will be associated with (eg. ".txt, .doc", without the quotes).|
|```-AppId <String>``` [optional] | Specifies a value to set Application Id to in the appx manifest. If it is not specified, it will be set to the value passed in for *PackageName*.|
|```-AppDisplayName <String>``` [optional] | Specifies a value to set Application Display Name to in the appx manifest. If it is not specified, it will be set to the value passed in for *PackageName*. |
|```-AppDescription <String>``` [optional] | Specifies a value to set Application Description to in the appx manifest. If it is not specified, it will be set to the value passed in for *PackageName*.|
|```-PackageDisplayName <String>``` [optional] | Specifies a value to set Package Display Name to in the appx manifest. If it is not specified, it will be set to the value passed in for *PackageName*. |
|```-PackagePublisherDisplayName <String>``` [optional] | Specifies a value to set Package Publisher Display Name to in the appx manifest. If it is not specified, it will be set to the value passed in for *Publisher*. |

### Other Conversion Parameters  
|Parameter|Description|
|---------|-----------|
|```-ExpandedBaseImage <String>``` [optional] | Full path to an already expanded base image.|
|```-MakeAppx [<SwitchParameter>]``` [optional] | A switch that, when present, tells this script to call MakeAppx on the output. |
|```-LogFile <String>``` [optional] | Specifies a log file. If omitted, a log file temporary location will be created. |
|```<Common parameters>``` | This cmdlet supports the common parameters: *Verbose*, *Debug*, *ErrorAction*, *ErrorVariable*, *WarningAction*, *WarningVariable*, *OutBuffer*, *PipelineVariable*, and *OutVariable*. For more info, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216). |

### Cleanup Parameters
|Parameter|Description|
|---------|-----------|
|```Cleanup [<Option>]``` | Runs cleanup for the DesktopAppConverter artifacts. There are 3 valid options for the Cleanup mode. |
|```Cleanup All``` | Deletes all expanded base images, removes any temporary converter files, removes the container network, and disables the optional Windows feature, Containers. |
|```Cleanup WorkDirectory``` | Removes all the temporary converter files. |
|```Cleanup ExpandedImages``` | Deletes all the expanded base images installed on your host machine. |

### x86 Package Parameters
The Desktop App Converter Preview now supports creation of x86 app packages that you can install and run on both x86 and amd64 machines. Note the Desktop App Converter still needs to run on an AMD64 machine to perform a successful conversion.

|Parameter|Description|
|---------|-----------|
|```-CreateX86Package[<SwitchParameter>]``` | Generates a 32-bit package that can install and run on both a 32-bit and 64-bit host OS. By default, converter attempts to detect package architecture from app’s main executable or defaults to 64-bit if no exe is found. |

## See also
+ [Get the Desktop App Converter](http://go.microsoft.com/fwlink/?LinkId=785437)
+ [Bring your desktop app to the Universal Windows Platform](https://developer.microsoft.com/en-us/windows/bridges/desktop)
+ [Bringing Desktop Apps to the UWP Using Desktop App Converter](https://channel9.msdn.com/events/Build/2016/P504)
+ [Project Centennial: Bringing Existing Desktop Applications to the Universal Windows Platform](https://channel9.msdn.com/events/Build/2016/B829)  
+ [UserVoice for Desktop Bridge (Project Centennial)](http://aka.ms/UserVoiceDesktopToUwp)
+ [Desktop app bridge to UWP code samples on GitHub](https://github.com/Microsoft/DesktopBridgeToUWP-Samples)


<!--HONumber=Jun16_HO3-->


