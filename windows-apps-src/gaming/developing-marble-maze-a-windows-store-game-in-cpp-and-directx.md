---
author: mtoepke
title: Developing Marble Maze, a UWP game in C++ and DirectX
description: This section of the documentation describes how to use DirectX and Visual C++ to create a 3-D Universal Windows Platform (UWP) game.
ms.assetid: 43f1977a-7e1d-614c-696e-7669dd8a9cc7
---

# Developing Marble Maze, a UWP game in C++ and DirectX


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


This section of the documentation describes how to use DirectX and Visual C++ to create a 3-D Universal Windows Platform (UWP) game. This documentation shows how to create a 3-D game named Marble Maze that embraces new form factors such as tablets and also works on traditional desktop and laptop PCs.

> **Note**   To download the Marble Maze source code, see [DirectX Marble Maze game sample](http://go.microsoft.com/fwlink/?LinkId=624011).

 

> **Important**  Marble Maze illustrates design patterns that we consider to be best practices for creating UWP games. You can adapt many of the implementation details to fit your own practices and the unique requirements of the game you are developing. Feel free to use different techniques or libraries when those better suit your needs. (However, always ensure that your code passes the Windows App Certification Kit.) When we consider a Marble Maze implementation to be essential for successful game development, we emphasize it in this documentation.

 

## Introducing Marble Maze


We chose Marble Maze because it is relatively basic, but still demonstrates the breadth of features that are found in most games. It shows how to use graphics, input handling, and audio. It also demonstrates game mechanics such as rules and goals.

Marble Maze resembles the table-top labyrinth game that is typically constructed from a box that contains holes and a steel or glass marble. The goal of Marble Maze is the same as the table-top version: tilt the maze to guide the marble from the start to the end of the maze in as little time as possible, without letting the marble fall into any of the holes. Marble Maze adds the concept of checkpoints. If the marble falls into a hole, the game is restarted at the last checkpoint location that the marble passed over.

Marble Maze offers multiple ways for a user to interact with the game board. If you have a touch-enabled or accelerometer-enabled device, you can use those devices to move the game board. You can also use an Xbox 360 controller or a mouse to control game play.

![screen shot of the marble maze game.](images/marblemaze.png)

## Prerequisites


-   Windows 10
-   Microsoft Visual Studio 2015
-   C++ programming knowledge
-   Familiarity with DirectX and DirectX terminology
-   Basic knowledge of COM

## Who should read this?


If you’re interested in creating 3-D games or other graphics-intensive applications for Windows 10, this is for you. We hope you use the principles and practices that this documentation outlines to create your own UWP game. A background or strong interest in C++ and DirectX programming will help you get the most out of this documentation. If you don't have experience with DirectX, you can still benefit if you have experience with similar 3-D graphics programming environments.

The document [Walkthrough: create a simple UWP game with DirectX](tutorial--create-your-first-metro-style-directx-game.md) describes another sample that implements a basic 3-D shooting game by using DirectX and C++.

## What this documentation covers


This documentation teaches how to:

-   Use the Windows Runtime API and DirectX to create a UWP game.
-   Use [Direct3D](https://msdn.microsoft.com/library/windows/desktop/ff476080) and [Direct2D](https://msdn.microsoft.com/library/windows/desktop/dd370990) to work with visual content such as models, textures, vertex and pixel shaders, and 2-D overlays.
-   Integrate input mechanisms such as touch, accelerometer, and the Xbox 360 controller.
-   Use [XAudio2](https://msdn.microsoft.com/library/windows/desktop/hh405049) to incorporate music and sound effects.

## What this documentation does not cover


This documentation does not cover the following aspects of game development. These aspects are followed by additional resources that cover them.

-   3-D game design principles.
-   C++ or DirectX programming basics.
-   How to design resources such as textures, models, or audio.
-   How to troubleshoot behavior or performance issues in your game.
-   How to prepare your game for use in other parts of the world.
-   How to certify and publish your game to the Windows Store.

Marble Maze also uses the [DirectXMath](https://msdn.microsoft.com/library/windows/desktop/hh437833) library to work with 3-D geometry and perform physics calculations, such as collisions. DirectXMath is not covered in-depth in this section. For more info about DirectXMath, see [DirectXMath Programming Guide](https://msdn.microsoft.com/library/windows/desktop/hh437833). For details about how Marble Maze uses DirectXMath, refer to the source code.

Although Marble Maze provides many reusable components, it is not a complete game development framework. When we consider a Marble Maze component to be reusable in your game, we emphasize it in the documentation.

## Next steps


We recommend that you start with Marble Maze sample fundamentals to learn about the Marble Maze structure and some of the coding and style guidelines that the Marble Maze source code follows. The following table outlines the documents in this section so that you can more easily refer to them.

## Related Topics


| Title                                                                                                                    | Description                                                                                                                                                                                                                                        |
|--------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Marble Maze sample fundamentals](marble-maze-sample-fundamentals.md)                                                   | Provides an overview of the game structure and some of the code and style guidelines that the source code follows.                                                                                                                                 |
| [Marble Maze application structure](marble-maze-application-structure.md)                                               | Describes how the Marble Maze application code is structured and how the structure of a DirectX UWP app differs from that of a traditional desktop application.                                                                                    |
| [Adding visual content to the Marble Maze sample](adding-visual-content-to-the-marble-maze-sample.md)                   | Describes some of the key practices to keep in mind when you work with Direct3D and Direct2D. Also describes how Marble Maze applies these practices for visual content.                                                                           |
| [Adding input and interactivity to the Marble Maze sample](adding-input-and-interactivity-to-the-marble-maze-sample.md) | Describes how Marble Maze works with accelerometer, touch, and Xbox 360 controller devices to enable users to navigate menus and interact with the game board. Also describes some of the best practices to keep in mind when you work with input. |
| [Adding audio to the Marble Maze sample](adding-audio-to-the-marble-maze-sample.md)                                     | Describes how Marble Maze works with audio to add music and sound effects to the game experience.                                                                                                                                                  |

 

 

 






<!--HONumber=Jun16_HO3-->


