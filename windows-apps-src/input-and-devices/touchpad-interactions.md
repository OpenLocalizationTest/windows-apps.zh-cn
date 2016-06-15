---
author: Karl-Bridge-Microsoft
Description: Create Universal Windows Platform (UWP) apps with intuitive and distinctive user interaction experiences that are optimized for touchpad but are functionally consistent across input devices.
title: Touchpad interactions
ms.assetid: CEDEA30A-FE94-4553-A7FB-6C1FA44F06AB
label: Touchpad interactions
template: detail.hbs
---

# Touchpad design guidelines


Design your app so that users can interact with it through a touchpad. A touchpad combines both indirect multi-touch input with the precision input of a pointing device, such as a mouse. This combination makes the touchpad suited to both a touch-optimized UI and the smaller targets of productivity apps.

 

![touchpad](images/input-patterns/input-touchpad.jpg)


Touchpad interactions require three things:

-   A standard touchpad or a Windows Precision Touchpad.

    Precision touchpads are optimized for Universal Windows Platform (UWP) devices. They enable the system to handle certain aspects of the touchpad experience natively, such as finger tracking and palm detection, for a more consistent experience across devices.

-   The direct contact of one or more fingers on the touchpad.
-   Movement of the touch contacts (or lack thereof, based on a time threshold).

The input data provided by the touchpad sensor can be:

-   Interpreted as a physical gesture for direct manipulation of one or more UI elements (such as panning, rotating, resizing, or moving). In contrast, interacting with an element through its properties window or other dialog box is considered indirect manipulation.
-   Recognized as an alternative input method, such as mouse or pen.
-   Used to complement or modify aspects of other input methods, such as smudging an ink stroke drawn with a pen.

A touchpad combines indirect multi-touch input with the precision input of a pointing device, such as a mouse. This combination makes the touchpad suited to both touch-optimized UI and the typically smaller targets of productivity apps and the desktop environment. Optimize your Windows Store app design for touch input and get touchpad support by default.

Because of the convergence of interaction experiences supported by touchpads, we recommend using the [**PointerEntered**](https://msdn.microsoft.com/library/windows/apps/br208968) event to provide mouse-style UI commands in addition to the built-in support for touch input. For example, use previous and next buttons to let users flip through pages of content as well as pan through the content.

The gestures and guidelines discussed in this topic can help to ensure that your app supports touchpad input seamlessly and with minimal code.

## <span id="The_touchpad_language"></span><span id="the_touchpad_language"></span><span id="THE_TOUCHPAD_LANGUAGE"></span>The touchpad language


A concise set of touchpad interactions are used consistently throughout the system. Optimize your app for touch and mouse input and this language makes your app feel instantly familiar for your users, increasing their confidence and making your app easier to learn and use.

Users can set far more Precision Touchpad gestures and interaction behaviors than they can for a standard touchpad. These two images show the different touchpad settings pages from Settings &gt; Devices &gt; Mouse & touchpad for a standard touchpad and a Precision Touchpad, respectively.

![standard touchpad settings](images/mouse-touchpad-settings-standard.png)

<sup>Standard\\ touchpad\\ settings</sup>

![windows precision touchpad settings](images/mouse-touchpad-settings-ptp.png)

<sup>Windows\\ Precision\\ Touchpad\\ settings</sup>

Here are some examples of touchpad-optimized gestures for performing common tasks.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Term</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Three-finger_tap"></span><span id="three-finger_tap"></span><span id="THREE-FINGER_TAP"></span>Three-finger tap</p></td>
<td align="left"><p>User preference to search with <strong>Cortana</strong> or show <strong>Action Center</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Three_finger_slide"></span><span id="three_finger_slide"></span><span id="THREE_FINGER_SLIDE"></span>Three finger slide</p></td>
<td align="left"><p>User preference to open the virtual desktop Task View, show Desktop, or switch between open apps.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Single_finger_tap_for_primary_action"></span><span id="single_finger_tap_for_primary_action"></span><span id="SINGLE_FINGER_TAP_FOR_PRIMARY_ACTION"></span>Single finger tap for primary action</p></td>
<td align="left"><p>Use a single finger to tap an element and invoke its primary action (such as launching an app or executing a command).</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Two_finger_tap_to_right-click"></span><span id="two_finger_tap_to_right-click"></span><span id="TWO_FINGER_TAP_TO_RIGHT-CLICK"></span>Two finger tap to right-click</p></td>
<td align="left"><p>Tap with two fingers simultaneously on an element to select it and display contextual commands.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Two_finger_slide_to_pan"></span><span id="two_finger_slide_to_pan"></span><span id="TWO_FINGER_SLIDE_TO_PAN"></span>Two finger slide to pan</p></td>
<td align="left"><p>Slide is used primarily for panning interactions but can also be used for moving, drawing, or writing.</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Pinch_and_stretch_to_zoom"></span><span id="pinch_and_stretch_to_zoom"></span><span id="PINCH_AND_STRETCH_TO_ZOOM"></span>Pinch and stretch to zoom</p></td>
<td align="left"><p>The pinch and stretch gestures are commonly used for resizing and Semantic Zoom.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Single_finger_press_and_slide_to_rearrange"></span><span id="single_finger_press_and_slide_to_rearrange"></span><span id="SINGLE_FINGER_PRESS_AND_SLIDE_TO_REARRANGE"></span>Single finger press and slide to rearrange</p></td>
<td align="left"><p>Drag an element.</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Single_finger_press_and_slide_to_select_text"></span><span id="single_finger_press_and_slide_to_select_text"></span><span id="SINGLE_FINGER_PRESS_AND_SLIDE_TO_SELECT_TEXT"></span>Single finger press and slide to select text</p></td>
<td align="left"><p>Press within selectable text and slide to select it. Double-tap to select a word.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Left_and_right_click_zone"></span><span id="left_and_right_click_zone"></span><span id="LEFT_AND_RIGHT_CLICK_ZONE"></span>Left and right click zone</p></td>
<td align="left"><p>Emulate the left and right button functionality of a mouse device.</p></td>
</tr>
</tbody>
</table>

 

## <span id="Hardware"></span><span id="hardware"></span><span id="HARDWARE"></span>Hardware


Query the mouse device capabilities ([**MouseCapabilities**](https://msdn.microsoft.com/library/windows/apps/br225626)) to identify what aspects of your app UI the touchpad hardware can access directly. We recommend providing UI for both touch and mouse input.

For more info about querying device capabilities, see [Identify input devices](identify-input-devices.md).

## <span id="Visual_feedback"></span><span id="visual_feedback"></span><span id="VISUAL_FEEDBACK"></span>Visual feedback


-   When a touchpad cursor is detected (through move or hover events), show mouse-specific UI to indicate functionality exposed by the element. If the touchpad cursor doesn't move for a certain amount of time, or if the user initiates a touch interaction, make the touchpad UI gradually fade away. This keeps the UI clean and uncluttered.
-   Don't use the cursor for hover feedback, the feedback provided by the element is sufficient (see [Cursors](#Cursors) below).
-   Don't display visual feedback if an element doesn't support interaction (such as static text).
-   Don't use focus rectangles with touchpad interactions. Reserve these for keyboard interactions.
-   Display visual feedback concurrently for all elements that represent the same input target.

For more general guidance about visual feedback, see [Guidelines for visual feedback](https://msdn.microsoft.com/library/windows/apps/hh465342).

## <span id="Cursors"></span><span id="cursors"></span><span id="CURSORS"></span>Cursors


A set of standard cursors is available for a touchpad pointer. These are used to indicate the primary action of an element.

Each standard cursor has a corresponding default image associated with it. The user or an app can replace the default image associated with any standard cursor at any time. Windows Store apps specify a cursor image through the [**PointerCursor**](https://msdn.microsoft.com/library/windows/apps/br208273) function.

If you need to customize the mouse cursor:

-   Always use the arrow cursor (![arrow cursor](images/cursor-arrow.png)) for clickable elements. don't use the pointing hand cursor (![pointing hand cursor](images/cursor-pointinghand.png)) for links or other interactive elements. Instead, use hover effects (described earlier).
-   Use the text cursor (![text cursor](images/cursor-text.png)) for selectable text.
-   Use the move cursor (![move cursor](images/cursor-move.png)) when moving is the primary action (such as dragging or cropping). Don't use the move cursor for elements where the primary action is navigation (such as Start tiles).
-   Use the horizontal, vertical and diagonal resize cursors (![vertical resize cursor](images/cursor-vertical.png), ![horizontal resize cursor](images/cursor-horizontal.png), ![diagonal resize cursor (lower left, upper right)](images/cursor-diagonal2.png), ![diagonal resize cursor (upper left, lower right)](images/cursor-diagonal1.png)), when an object is resizable.
-   Use the grasping hand cursors (![grasping hand cursor (open)](images/cursor-pan1.png), ![grasping hand cursor (closed)](images/cursor-pan2.png)) when panning content within a fixed canvas (such as a map).

## <span id="related_topics"></span>Related articles


* [Handle pointer input](handle-pointer-input.md)
* [Identify input devices](identify-input-devices.md)
            
          
            **Samples**
* [Basic input sample](http://go.microsoft.com/fwlink/p/?LinkID=620302)
* [Low latency input sample](http://go.microsoft.com/fwlink/p/?LinkID=620304)
* [User interaction mode sample](http://go.microsoft.com/fwlink/p/?LinkID=619894)
* [Focus visuals sample](http://go.microsoft.com/fwlink/p/?LinkID=619895)
            
          
            **Archive Samples**
* [Input: Device capabilities sample](http://go.microsoft.com/fwlink/p/?linkid=231530)
* [Input: XAML user input events sample](http://go.microsoft.com/fwlink/p/?linkid=226855)
* [XAML scrolling, panning, and zooming sample](http://go.microsoft.com/fwlink/p/?linkid=251717)
* [Input: Gestures and manipulations with GestureRecognizer](http://go.microsoft.com/fwlink/p/?LinkID=231605)
 





<!--HONumber=Jun16_HO2-->

