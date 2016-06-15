---
author: mcleanbyron
ms.assetid: 2ed21281-f996-402d-a968-d1320a4691df
description: Use the test application ID and ad unit ID values from this article to see how your app renders ads during testing.
title: Test mode values
---

# Test mode values


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

When you use an [AdControl](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.adcontrol.aspx) or [InterstitialAd](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.interstitialad.aspx)  to display ads in your app, you must specify an application ID and ad unit ID. While you are developing your app, use the test application ID and ad unit ID values from this article to see how your app renders ads during testing.

> **Important**   If your app uses ad mediation (that is, it uses an **AdMediatorControl** object), you do not need to specify ad units. In this scenario, ad units are automatically generated for you. For more information, see [What is the difference: AdMediatorControl or AdControl](what-is-the-difference-admediatorcontrol-or-adcontrol.md).

If you try to use test values in your app after you publish it, your live app not receive ads. To receive ads in your published app, you must update your code to use an application ID and ad unit ID provided by the Windows Dev Center dashboard. For more information, see [Set up ad units in your app](set-up-ad-units-in-your-app.md).
 

Here are the test values to use for video interstitial and banner ads.

* For video interstitial ads:

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">AdUnitId</th>
    <th align="left">AppId</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>11389925</p></td>
    <td align="left"><p>d25517cb-12d4-4699-8bdc-52040c712cab</p></td>
    </tr>
    </tbody>
    </table>

     
* For banner ads:

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">AdUnitId</th>
    <th align="left">AppId</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>10865270</p></td>
    <td align="left"><p>3f83fe91-d6be-434d-a0ae-7351c5a997f1</p></td>
    </tr>
    </tbody>
    </table>


> **Important**   The size of a live ad is defined by the **Width** and **Height** properties of the **AdControl**. For best results, make sure that the **Width** and **Height** properties in your code are one of the [supported ad sizes for banner ads](supported-ad-sizes-for-banner-ads.md). The **Width** and **Height** properties will not change based on the size of a live ad.



 

 


<!--HONumber=Jun16_HO2-->


