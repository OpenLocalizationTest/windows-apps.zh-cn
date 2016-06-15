---
author: DelfCo
ms.assetid: 2CC2E526-DACB-4008-9539-DA3D0C190290
description: A quick overview of the networking technologies available for a UWP developer, with suggestions on how to choose the technologies that are right for your app.
title: Which networking technology?'

---

# Which networking technology?

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

A quick overview of the networking technologies available for a UWP developer, with suggestions on how to choose the technologies that are right for your app.

## Sockets

Use [Sockets](sockets.md) when you are communicating with another device and want to use your own protocol.

Two implementations of sockets are available for Universal Windows Platform (UWP) developers: [**Windows.Networking.Sockets**](https://msdn.microsoft.com/library/windows/apps/br226960), and [Winsock](https://msdn.microsoft.com/library/windows/desktop/ms740673). If you are writing new code, then Windows.Networking.Sockets has the advantage of being a modern API, designed for use by UWP developers. If you are using cross-platform networking libraries or other existing Winsock code, or prefer the Winsock API, then use that.

### When to use sockets

-   Both sockets implementations enable you to communicate with other devices using protocols of your own choice, using TCP or UDP.

-   Choose the sockets API that best meets your needs based on experience and any existing code you might be using.

### When not to use sockets

-   Don't implement your own HTTP(S) stack using sockets. Use [**HttpClient**](https://msdn.microsoft.com/library/windows/apps/dn298639) instead.
-   If WebSockets (the [**StreamWebSocket**](https://msdn.microsoft.com/library/windows/apps/br226923) and [**MessageWebSocket**](https://msdn.microsoft.com/library/windows/apps/br226842) classes) meet your communications needs (TCP to/from a web server), consider using them rather than spend your own time and development resources implementing similar functionality with sockets.

## Websockets

The [WebSockets](websockets.md) protocol defines a mechanism for fast, secure two-way communication between a client and a server over the web. Data is transferred immediately over a full-duplex single socket connection, allowing messages to be sent and received from both endpoints in real time. WebSockets are ideal for use in real-time gaming where instant social network notifications and up-to-date displays of information (like game statistics ) need to be secure and use fast data transfer. UWP developers can use the [**StreamWebSocket**](https://msdn.microsoft.com/library/windows/apps/br226923) and [**MessageWebSocket**](https://msdn.microsoft.com/library/windows/apps/br226842) classes to connect with servers that support the Websocket protocol.

### When to use Websockets

-   When you want to send and receive data on an ongoing basis between a device and a server.

### When not to use Websockets

-   If you are sending or receiving data infrequently, you might find it simpler to make individual HTTP requests from the device to the server, rather than establish and maintain a WebSocket connection.
-   WebSockets may not be suitable for very high-volume situations. Consider modeling your data flows and simulating your traffic through WebSockets before committing to using them in your design.

## HttpClient

Use [HttpClient](httpclient.md) (and the rest of the [**Windows.Web.Http**](https://msdn.microsoft.com/library/windows/apps/dn279692) namespace API) when you are using HTTP(S) to communicate with a web service or a web server.

### When to use HttpClient

-   When using HTTP(S) to communicate with web services.
-   When uploading or downloading a small number of smaller files.
-   If WebSockets (the [**StreamWebSocket**](https://msdn.microsoft.com/library/windows/apps/br226923) and [**MessageWebSocket**](https://msdn.microsoft.com/library/windows/apps/br226842) classes) meet your communications needs (TCP to/from a web server), and the web server in question supports WebSockets, consider using them rather than spend your own time and development resources implementing similar functionality with HttpClient.
-   When you are streaming content over the network.

### When not to use HttpClient

-   If you are transferring large files, or large numbers of files, consider using background transfers instead.
-   If you want to be able to restrict upload/download limits based on connection type, or if you want to save progress and resume upload/download after an interruption, you must use background transfers.
-   If you are communicating between two devices and neither one is designed to act as an HTTP(S) server, you should use sockets. Do not attempt to implement your own HTTP server and use [HttpClient](httpclient.md) to communicate with it.

## Background transfers

Use the [background transfer API](background-transfers.md) when you want to reliably transfer files over the network. The background transfer API provides advanced upload and download features that run in the background during app suspension and persist beyond app termination. The API monitors network status and automatically suspends and resumes transfers when connectivity is lost, and transfers are also Data Sense-aware and Battery Sense-aware, meaning that download activity adjusts based on your current connectivity and device battery status. These capabilities are essential when your app is running on mobile or battery-powered devices. The API is ideal for uploading and downloading large files using HTTP(S). FTP is also supported, but only for downloads.

A new background transfer feature in Windows 10 is the ability to trigger post-processing when a file transfer has completed, so that you can update local catalogs, activate other apps, or notify the user when a download is complete.

### When to use background transfers

-   Use background transfers to reliably transfer large files, or large numbers of files.
-   Use background transfers with background transfer completion groups when you want to post-process file transfers with a background task.
-   Use background transfers if you want to be able to resume a transfer in progress after a network interruption.
-   Use background transfers if you want to be able to change transfer behavior based on network conditions like being on a metered data plan.

### When not to use background transfers

-   If you are transferring a small number of small files, and you don't need to do any post-processing when the transfer is complete, consider using [**HttpClient**](https://msdn.microsoft.com/library/windows/apps/dn298639) PUT or POST methods.
-   If you want to stream data and use it locally as it arrives, use [**HttpClient**](https://msdn.microsoft.com/library/windows/apps/dn298639).

## Additional network-related technologies

### Connection quality

The [**Windows.Networking.Connectivity**](https://msdn.microsoft.com/library/windows/apps/br207308) API enables you to access network connectivity, cost, and usage information. For more information about using this API, see [Accessing network connection state and managing network costs](https://msdn.microsoft.com/library/windows/apps/hh452983)

### DNS Service Discovery

The [**Windows.Networking.ServiceDiscovery.Dnssd**](https://msdn.microsoft.com/library/windows/apps/dn895183) API enables you to advertise a network service to other devices on the network using the DNS-SD protocol described in IETF [RFC 2782](http://go.microsoft.com/fwlink/?LinkId=524158).

### Communicating over Bluetooth

Among other things, the [**Windows.Devices.Bluetooth**](https://msdn.microsoft.com/library/windows/apps/dn263413) API enables you to use Bluetooth to connect to other devices and transfer data. For more information, see [Send or receive files with RFCOMM](https://msdn.microsoft.com/library/windows/apps/mt270289).

### Push notifications (WNS)

The [**Windows.Networking.PushNotifications**](https://msdn.microsoft.com/library/windows/apps/br241307) API enables you to use the Windows Notification Service (WNS) to receive push notifications over the network. For more information about using this API, see [Windows Push Notification Services (WNS) overview](https://msdn.microsoft.com/library/windows/apps/mt187203)

### Near field communications

The [**Windows.Networking.Proximity**](https://msdn.microsoft.com/library/windows/apps/br241250) API enables you to use near-field communications for apps that use proximity or tap with devices to enable easy data transfer. For more information about using this API, see [Supporting proximity and tapping](https://msdn.microsoft.com/library/windows/apps/hh465229).

### RSS/Atom feeds

The [**Windows.Web.Syndication**](https://msdn.microsoft.com/library/windows/apps/br243632) API enables you to manage syndication feeds using RSS and Atom formats. For more information about using this API, see [RSS/Atom feeds](web-feeds.md).

### Wi-Fi enumeration and connection control

The [**Windows.Devices.WiFi**](https://msdn.microsoft.com/library/windows/apps/dn975224) API enables you to enumerate Wi-Fi adapters, scan for available Wi-Fi networks, and connect an adapter to a network.

### Radio control

The [**Windows.Devices.Radios**](https://msdn.microsoft.com/library/windows/apps/dn996447) API allows you to find and control radios on the local device, including Wi-Fi and Bluetooth.

### Wi-Fi Direct

The [**Windows.Devices.WiFiDirect**](https://msdn.microsoft.com/library/windows/apps/dn297687) API allows you to connect and communicate with other local devices using Wi-Fi Direct to create ad-hoc local wireless networks.

### Wi-Fi Direct services

The [**Windows.Devices.WiFiDirect.Services**](https://msdn.microsoft.com/library/windows/apps/dn996481) API enables you to provide Wi-Fi Direct services and connect to them. Wi-Fi Direct Services are the way that one device on a Wi-Fi direct ad-hoc network (a Service Advertiser) offers capabilities to another device (a Service Seeker) over a Wi-Fi Direct connection.

### Mobile operators

Windows 10 exposes to a wide developer audience some APIs that have previously only been exposed to device manufacturers and mobile operators. Note that while these APIs are exposed now, they are also gated by specific app capabilities that must be approved by Microsoft before an app can be published. Actual use of these APIs will still be limited primarily to device manufacturers and mobile operators.

### Network operations

The [**Windows.Networking.NetworkOperators**](https://msdn.microsoft.com/library/windows/apps/br241148) API deals primarily with the configuration and provisioning of phones. As such, permission to use the capabilities that control it are limited to device manufacturers and telecom providers.

### SMS

The [**Windows.Devices.Sms**](https://msdn.microsoft.com/library/windows/apps/br206567) namespace deals with SMS and related messages as low-level entities. It is provided for use by mobile operators for app-directed SMS use, and is controlled by a capability that will not be approved for use by most app developers. If you are writing an app to deal with messages, you should use the [**Windows.ApplicationModel.Chat**](https://msdn.microsoft.com/library/windows/apps/dn642321) API instead, as it is designed to handle not just SMS messages, but also messages from other sources such as realtime chat apps, enabling a much richer chat/messaging experience.



<!--HONumber=Jun16_HO2-->

