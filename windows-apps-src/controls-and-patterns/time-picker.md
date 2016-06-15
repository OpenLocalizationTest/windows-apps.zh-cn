---
author: Jwmsft
Description: The time picker gives you a standardized way to let users pick a time value using touch, mouse, or keyboard input.
title: Time picker
ms.assetid: 5124ecda-09e6-449e-9d4a-d969dca46aa3
label: Time picker
template: detail.hbs
---

# Time picker

The time picker gives you a standardized way to let users pick a time value using touch, mouse, or keyboard input. 

<span class="sidebar_heading" style="font-weight: bold;">Important APIs</span>

-   [**TimePicker class**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.timepicker.aspx)
-   [**Time property**](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.timepicker.time.aspx)

## Is this the right control?
Use a time picker to let a user pick a single time value.

For more info about choosing the right control, see the [Date and time controls](date-and-time.md) article.

## Examples

The entry point displays the chosen time, and when the user selects the entry point, a picker surface expands vertically from the middle for the user to make a selection. The time picker overlays other UI; it doesn't push other UI out of the way.

![Example of the time picker expanding](images/controls_timepicker_expand.png)

## Create a time picker

This example shows how to create a simple time picker with a header.

```xaml
<TimePicker x:Name=arrivalTimePicker Header="Arrival time"/>
```

```csharp
TimePicker arrivalTimePicker = new TimePicker();
arrivalTimePicker.Header = "Arrival time";
```

The resulting time picker looks like this:

![Example of time picker](images/time-picker-closed.png)

> **Note**
            &nbsp;&nbsp;For important info about date and time values, see [DateTime and Calendar values](date-and-time.md#datetime-and-calendar-values) in the *Date and time controls* article.



## Related topics

- [Date and time controls](date-and-time.md)
- [Calendar date picker](calendar-date-picker.md)
- [Calendar view](calendar-view.md)
- [Date picker](date-picker.md)


<!--HONumber=Jun16_HO2-->


