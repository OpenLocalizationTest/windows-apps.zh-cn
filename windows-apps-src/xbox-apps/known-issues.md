---
author: Mtoepke
title: Known issues with UWP on Xbox One developer preview
description: 
area: Xbox
---

# Known issues with UWP on Xbox developer preview

This topic describes known issues with the UWP on Xbox developer preview. For more information about this developer preview, see [UWP on Xbox](index.md). 

\[If you came here from a link in an API reference topic, and are looking for Universal device family API information, please see [UWP features that aren't yet supported on Xbox](http://go.microsoft.com/fwlink/?LinkID=760755).\]

The Xbox Developer Preview System Update includes experimental and early pre-release software. This means that some popular games and apps will not work as expected, and you may experience occasional crashes and data loss. If you leave the developer preview, your console will factory reset and you will have to reinstall all of your games, apps, and content.

For developers, this means that not all developer tools and APIs will function as expected. Not all features intended for the final release are included or are at release quality. 
**In particular, system performance in this preview does not reflect system performance of the final release.**

The following list highlights some known issues that you might encounter in this release, but this list is not exhaustive. 

**We want to get your feedback**, so please report any issues that you find on the [Developing Universal Windows apps](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/home?forum=wpdevelop) forum. 

If you get stuck, read the information in this topic, see [Frequently asked questions](frequently-asked-questions.md), and use the forums to ask for help.


## Developing games

### Mouse mode support

For information about _mouse mode_ support, see the [Designing for Xbox and TV](https://msdn.microsoft.com/en-us/windows/uwp/input-and-devices/designing-for-tv?f=255&MSPPError=-2147217396#mouse-mode) topic. This topic includes information about how to enable and disable mouse mode, so you can choose the right behavior for your app. 

<!--### x86 vs. x64

By the time we release later this year, we will have great support for both x86 and x64, and we do support x86 in this preview. 
However, x64 has had much more testing to date (the Xbox shell and all of the apps running on the console today are x64), and so we recommend using x64 for your projects. 
This is particularly true for games.

If you decide to use x86, please report any issues you see on the forum.

Also see [Switching build flavors can cause deployment failures](known-issues.md#switching-build-flavors-can-cause-deployment-failures) later on this page.-->

<!--### Game engines

We have tested some popular game engines, but not all of them, and our test coverage for this preview has not been comprehensive. 
Your mileage may vary. 

The following game engines have been confirmed to work:
* [Construct 2](https://www.scirra.com/)

There are likely others that are working too. We would love to get your feedback on what you find. 
Please use the forum to report any issues you see.-->

### DirectX 12 support

UWP on Xbox One supports DirectX 11 Feature Level 10. DirectX 12 is not supported at this time. Xbox One, like all traditional games consoles, is a specialized piece of hardware that requires a specific SDK to access its full potential. If you are working on a game that requires access to the maximum potential of the Xbox One hardware, you can register with the [ID@XBOX](http://www.xbox.com/en-us/Developers/id) program to get access to that SDK, which includes DirectX 12 support.

<!-- ### Xbox One Developer Preview disables game streaming to Windows 10

Activating the Xbox One Developer Preview on your console will prevent you from streaming games from your Xbox One to the Xbox app on Windows 10, even if your console is set to retail mode. 
To restore the game streaming feature, you must leave the developer preview. -->

### Known issue with the TV safe area

By default, the display area for UWP apps on Xbox should be inset by the TV safe area. However, the Xbox One Developer Preview contains a known bug that causes the TV safe area to start at [0, 0] rather than at [_offset_, _offset_].

For more information about the TV safe area, see [Designing for Xbox and TV](https://msdn.microsoft.com/windows/uwp/input-and-devices/designing-for-tv). 

The easiest way to work around this issue is to disable the TV safe area, as shown in the following JavaScript example.

    var applicationView = Windows.UI.ViewManagement.ApplicationView.getForCurrentView();

    applicationView.setDesiredBoundsMode(Windows.UI.ViewManagement.ApplicationViewBoundsMode.useCoreWindow);

<!--## System resources for UWP apps and games on Xbox One

UWP apps and games running on Xbox One share resources with the system and other apps, and so the system governs the resources that are available to any one game or app. 
If you are running into memory or performance issues, this may be why. 
For more details, see [System resources for UWP apps and games on Xbox One](system-resource-allocation.md).-->


## Networking using traditional sockets

In this developer preview, inbound and outbound network access from the console that uses traditional TCP/UDP sockets (WinSock, Windows.Networking.Sockets) is not available. Developers can still use HTTP and WebSockets. 


## UWP API coverage

Not all UWP APIs work as intended on Xbox in this preview. See [UWP features that aren't yet supported on Xbox](http://go.microsoft.com/fwlink/p/?LinkId=760755) for the list of APIs that we know don’t work. If you find issues with other APIs, please report them on the forums. 

<!--## XAML controls do not look like or behave like the controls in the Xbox One shell

In this developer preview, the XAML controls are not in their final form. In particular:
* Gamepad X-Y navigation does not work reliably for all controls.
* Controls do not look like controls in the Xbox shell. This includes the control focus rectangle.
* Navigating between controls does not automatically make “navigation sounds.”

These issues will be addressed in a future developer preview.-->

<!--## Visual Studio and deployment issues

### Switching build flavors can cause deployment failures

Switching between Debug and Release builds, or between x86 and x64, or between Managed and .Net Native builds, can cause deployment failures. 

The simplest way to avoid these issues for this preview is to stick to Debug and one architecture. 

If you do hit this issue, uninstalling your app in the Collections app on your Xbox One will typically resolve it.

> ****&nbsp;&nbsp;Uninstalling your app from Windows Device Portal (WDP) will not resolve the issue.

If your issues persist, uninstall your app or game in the Collections app, leave Developer Mode, restart to Retail Mode and then switch back to Developer Mode.
You may also need to restart Visual Studio and clean your solution.

For more information, see the “Fixing deployment failures” section in [Frequently asked questions](frequently-asked-questions.md).

### Uninstalling an app while you are debugging it in Visual Studio will cause it to fail silently

Attempting to uninstall an app that is running under the debugger via the WDP “Installed Apps” tool will cause it to silently fail. 
The workaround is to stop debugging the app in Visual Studio before attempting to remove it via WDP.

### Visual Studio/Xbox PIN pairing failures

It is possible to get into a state where the PIN pairing between Visual Studio and your Xbox One gets out of sync. 
If PIN pairing fails, use the “Remove all pairings” button in Dev Home, restart Xbox One, restart your development PC, and then try again.--> 


## Windows Device Portal (WDP) preview

<!--### Starting WDP from Dev Home crashes Dev Home

When you start WDP in Dev Home, it will cause Dev Home to crash after you have entered your user name and password and selected **Save**. 
The credentials are saved but WDP is not started. 
You can start WDP by restarting Xbox One.--> 

<!--### Disabling WDP in Dev Home does not work

If you disable WDP in Dev Home, it will be turned off. 
However, when you restart your Xbox One, WDP will be started again. 
You can work around this issue by using **Reset and keep my games & apps** to delete any stored state on your Xbox One. 
Go to Settings > System > Console info & updates > Reset console, and then select the **Reset and keep my games & apps** button.

> **Caution**&nbsp;&nbsp;Doing this will delete all saved settings on your Xbox One including wireless settings, user accounts and any game progress that has not been saved to cloud storage.

> **Caution**&nbsp;&nbsp;DO NOT select the **Reset and remove everything** button.
This will delete all of your games, apps, settings and content, deactivate Developer Mode, and remove you console from the Developer Preview group.

### The columns in the “Running Apps” table do not update predictably. 

Sometimes this is resolved by sorting a column on the table.-->

### WDP UI does not display correctly in Internet Explorer 7 

By default, WDP UI does not display correctly in the browser when using Internet Explorer 7. You can fix this by turning off Internet Explorer 7’s Compatibility View for WDP.

### Navigating to WDP causes a certificate warning

You will receive a warning about the certificate that was provided, similar to the following screenshot, because the security certificate signed by your Xbox One console is not considered a well-known trusted publisher. Click "Continue to this website" to access the Windows Device Portal.

![Website security certificate warning](images/security_cert_warning.jpg)

<!--## Dev Home

Occasionally, selecting the “Manage Windows Device Portal” option in Dev Home will cause Dev Home to silently exit to the Home screen. 
This is caused by a failure in the WDP infrastructure on the console and can be resolved by restarting the console.-->

## See also
- [Frequently asked questions](frequently-asked-questions.md)
- [UWP on Xbox One](index.md)


<!--HONumber=Jun16_HO3-->


