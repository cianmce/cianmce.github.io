---
title: "Slaze"
date: 2014-12-17
draft: false
description: "Slaze in a Survival horror single player game modeled on the story of Slender Man."
summary: "Slaze in a Survival horror single player game modeled on the story of Slender Man."

tags: ["videogame", "opengl"]
---


<span class="preview">

  ![Slaze Gameplay](img/slaze_gameplay.png)

  Slaze in a Survival horror single player game modeled on the story of Slender Man, a tall, thin, faceless man who follows you at a distance but is never seen moving.

</span>

<!--more-->
{{< katex >}}

![Slaze Gameplay](img/slaze.png)

## Overview

Slaze in a Survival horror single player game modeled on the story of Slender Man, a tall, thin, faceless man who follows you at a distance but is never seen moving.

The game involves navigating through a randomly generated 3D maze while avoiding being caught by Slender and completing the levels tasks. All code for the game was with in C++ with OpenGL and GLSL for the Graphics Shaders using my own games engine over the course of 4 days.


{{< youtube MBXptMvaE7k >}}


## Game mechanics

Quaternion navigation was used with WASD and the Arrow Keys.

The equation of motion was used with gravity to model jumping with a small _spring_ was added before takeoff and after landing to simulate legs. A _bobbing_ up and down was added to give the effect of walking on an uneven surface.


## Lighting


[Phong Lighting](https://en.wikipedia.org/wiki/Phong_reflection_model) was used to give a realistic effect when light hit surfaces. A spotlight effect was used to simulate a flashlight. This light slowly ran out of battery making it dimmer and decreasing its radius. These were both implemented in the fragment shaders.

The amount of fog was increased as you progress through the game.

Just before getting caught by Slender there would be distortion in both the audio and video of the camera. I wanted to make random white noise appear on screan using a shader.

Shaders are unable to produce true randomness, so a pseudo-random number generator was created that produces a number from 0 to 1.


\\n = (43758.5 * sin(12.9898x + 78.233y + 1.532t)) \mod 1\\)


![Shader White Noise](img/slaze_shader_noise.png '[<i class="fa-solid fa-chart-column"></i> Wolfram Alpha rendering](https://www.wolframalpha.com/input?i=plot+%7C+%2843758.5+sin%2812.9898+x+%2B+78.233+y%29%29+mod+1+%7C+x+%3D+0+to+2+y+%3D+0+to+2)')

Using the above formula, a screen coordinate (**x** & **y**) and current time (**t**) was used to generate a random number. This was then used to create the illusion of camera white noise which can be seen below.

![Slaze Gameplay](img/slaze_gameplay.png)

For audio distortion I created high pitch scream noises using Audacity.


## Maze

Every time the game is played a random maze is produced for a given Size, Complexity and Density depending on the level. Complexity being essentially how long each wall is as a maze with shorted walls is not very complex whereas one with long walls and only one or two paths through is much more complex. And Density being how much of blank space is filled. 4 randomly generated mazes are shown below.


![Slaze Ascii Map](img/slaze_ascii_maze.png)

Ensuring the maze was solvable and every point was reachable was obviously important. To ensure this I placed a random cell wall then expanded in a random direction checking that 2 ahead was free. This ensured that there was always corridors and no closed loops.

Various different textures were randomly used for the walls, some plain and some with either blood, rust or graffiti on it.


## Collisions

Collisions were used to detect if you collided with a wall, lever, ending door or Slender.

When randomly moving Slender collisions were also checked.

## Texture & Models

All textures and models were created with Gimp and Blender.

Most models had a diffuse, ambient, specular and emission textures which were used in the fragment shader.

## Levels

Slaze can easily customized to have _N_ levels. It was found the 4 levels was a good number with a full game play lasting 10-20mins. Each level becomes more difficult than the one before.

The 4 levels were:

1. Little fog. Small maze. You, Slender, End, Lever & Walls on map
2. More fog. Bigger maze. You, End & Walls on map
3. More fog. Bigger maze. End & Walls on map
4. MORE FOG. HUGE maze. NO MAP!

For each size of the map the terrain mesh and it’s texture re-sized and scaled to perfectly fit edge to edge with the new width and height of the maze.

## Sound

Sound was a big part of my game. There is a consistent eerie noise playing in the background. Whenever Slender moves there’s 2 loud footsteps thumps. When seen a loud screech noise is played. 2 sounds were assigned to the operation of the lever happening one after the other making a grinding gear noise followed by an opening noise. A clicking noise is played when the flashlight is switched on or off.


## Performance

Various performance were kept in mind making the this game. They include loading GUIs and Sounds first so there’s something displayed to the user while they wait.

A radius around the camera was used to decide if an object should be drawn. In [this video](https://youtu.be/m1Yx7iGA8cY) a very small radius is used to demonstrate it



## Extra Links

Battery Recharging

 - http://youtu.be/TmP2W_mjgys

Intro

 - http://youtu.be/fmcseRKbw-I

Following + Animation

 - http://youtu.be/3YOasOncnu4

Drawing Radius

 - http://youtu.be/m1Yx7iGA8cY

Full Playthroughs

 - http://youtu.be/MBXptMvaE7k
 - http://youtu.be/Ynb7W2siZyg

Speedrun

 - http://youtu.be/WEn7s0wHsK8

