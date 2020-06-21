---
layout: post
title: Explosive
---

`C# | Unity`
<!-- excerpt -->

**DESCRIPTION**

In this puzzle-based game, the player's objective is to create an explosive using the chemicals provided in the laboratory. He or she must place each chemical on a pad, sometimes having to rotate or scale it beforehand. If all the chemicals are in their right places, the explosive appears.

**TECHNICAL BREAKDOWN**

***Object Selection***

An object is selected when the player hovers the mouse cursor over an object and clicks.

**Note**: All objects (i.e chemicals) are assigned a tag name *Selectable*

**PlayerObjectSelection.cs**

    1. Project a ray using Unity's built-in Physics engine
        1. If the object is a selectable object
            1. Display the reticle underneath the object
            2. If the player clicks on the mouse and there is no other object selected
                1. Select the object

![Selecting an object](/assets/images/ePlayerObjSelection.png)

***Object Manipulation***

An object can be manipulated in terms of its orientiation (X or Z axis) and scale (X, Y, or Z axis).

**Note**: The keys used to initiate rotation or scale of the object are R and T respectively

**PlayerObjectManipulation.cs**

Rotation

    1. If the R key is pressed and the object is not in scale mode
        1. Disable player rotation and movement

        2. Get the value of the virtual mouse X and Y axes as identified by Unity's Input System
        3. Subtract the value of the virtual mouse X axis from the selected game object's current Z orientiation (i.e Z orientation - virtual mouse X)
        4. Add the selected game object's current X orientiation to the value of the virtual mouse Y axis (i.e X orientation + virtual mouse Y)

        5. Restrict rotational range from -90 to 90 degrees on both the X and Z axis

        6. Rotate the selected object along its X and Z axes using Quaternions

Scale

    1. If the T key is pressed and the object is not in rotation mode
        1. Get the current local scale of the selected object and store it in a temporary variable

        2. If the X key is pressed
            1. Increase the width of the temporary scale by some factor

        3. If the Y key is pressed
            1. Increase the height of the temporary scale by some factor

        4. If the Z key is pressed
            1. Increase the depth of the temporary scale by some factor

        5. Update the seleced object's local scale with the new scale

![Manipulating an object](/assets/images/ePlayerObjManipulation.png)

***Spawning of the Explosive***

The explosive is spawned after the appropriate objects (i.e chemicals) have been placed on their pads.

**Note**: the *Pad.cs* script component is attached to each pad game object

**Pad.cs**

    1. Declare an OnTriggerEnter function in the script
        1. If the object that triggered the collision was a chemical and the pad has not yet been pressed
            1. Check if the color of the chemical is the same as the pad
                1. Declare the pad as activated (i.e that it has been pressed)
                2. Declare a count variable that will hold the total number of pads activated
                3. For each pad object in the game
                    1. Check if the pad has been activated
                        1. If it has, increase the count
                            1. Check if count is equal to the total number of pads in the game
                                1. If true, spawn the explosive at some position in the game (ex. a target platform)

![Spawning of the explosive](https://mantaevvfl.github.io/portfolio/assets/images/eSpawnExplosive.png)

**DEMO**

<iframe width="560" height="315" src="https://www.youtube.com/embed/8iCBh3TmW9A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>