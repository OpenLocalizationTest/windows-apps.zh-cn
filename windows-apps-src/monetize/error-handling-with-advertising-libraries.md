---
author: mcleanbyron
ms.assetid: cb7380d0-bc14-4936-aa1c-206304b3dc70
description: Learn how to handle errors that are generated by the AdControl class in the Microsoft advertising libraries.
title: Error handling with the Microsoft advertising libraries
---

# Error handling with the Microsoft advertising libraries


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

This topic provides basic information about how to handle errors that are generated by the [AdControl](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.adcontrol.aspx) class in the Microsoft advertising libraries.

<span id="bkmk-javascript"/>
## JavaScript/HTML apps

To handle **AdControl** errors in a JavaScript app:

1.  Assign the **onErrorOccurred** event to an event handler.

2.  Code the event handler.

The **onErrorOccurred** event handler is set in the **data-win-options** attribute for the **div** of the **AdControl**. In the following example, the **onErrorOccurred** event is set to be handled by a function named **errorLogger**.

``` syntax
<div id="myAd" style="position: absolute; top: 53px; left: 0px; width: 250px; height: 250px; z-index: 1"
     data-win-control="MicrosoftNSJS.Advertising.AdControl"
     data-win-options="{applicationId: 'd25517cb-12d4-4699-8bdc-52040c712cab', adUnitId: 'ADPT33', onErrorOccurred: errorLogger}">
</div>
```

The error handling function is declarative and must be enclosed in the [markSupportedForProcessing](http://msdn.microsoft.com/library/windows/apps/Hh967819.aspx) function.

The error handler catches the JavaScript error object when an **AdControl** error occurs. The error object provides two arguments to the error handler. For more information, see [Special Error Properties from Asynchronous Windows Runtime Methods](http://msdn.microsoft.com/library/windows/apps/hh994690.aspx).

Here is an example of an error handling function named **errorLogger** that handles the **onErrorOccurred** event.

``` syntax
WinJS.Utilities.markSupportedForProcessing(
window.errorLogger = function (sender, evt) {
    console.log(new Date()).toLocaleTimeString() + ": " + sender.element.id + " error: " + evt.errorMessage + " error code: " + evt.errorCode + \n");
});
```

See [Error Handling in JavaScript walkthrough](error-handling-in-javascript-walkthrough.md) for a walkthrough that demonstrates **AdControl** error handling in JavaScript.

<span id="bkmk-dotnet"/>
## XAML apps

To handle **AdControl** errors in a XAML app:

* Assign the **ErrorOccurred** event to the name of an event handler delegate.

* Code the error event handling delegate so that it takes two parameters: an **Object** for the sender and an **AdErrorEventArgs** object.

Here is an example that assigns a delegate named **OnAdError** to the **ErrorOccurred** event.

``` syntax
this.ErrorOccurred = OnAdError;
```

Here is an example definition of the **OnAdError** delegate that writes error information to the output window in Visual Studio.

``` syntax
private void OnAdError(object sender, AdErrorEventArgs e)
{
    System.Diagnostics.Debug.WriteLine("AdControl error (" + ((AdControl)sender).Name + "): " + e.Error + " ErrorCode: " + e.ErrorCode.ToString());
}
```

See [Error handling in XAML/C# walkthrough](error-handling-in-xamlc-walkthrough.md) for a walkthrough that demonstrates **AdControl** error handling in XAML and C#.

 

 


<!--HONumber=Jun16_HO2-->

