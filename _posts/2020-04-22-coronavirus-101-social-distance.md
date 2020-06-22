---
layout: post
title: 'Coronavirus 101: Social Distance'
---

`Processing`
<!-- excerpt -->

**DESCRIPTION**

A strategy game where the player protects a group of civilians from the coronavirus by guiding them towards uninfected platforms for as long as needed.

**TECHNICAL BREAKDOWN**

***Player Movement***

The player (along with the group of civilians) can move either left, right, up, or down but only onto platforms that are not infected.

**Main.pde**

**Note**: The platforms are represented as a two-dimensional array

The player moves using the WASD keys.

    1. If the W key is pressed
        1. Move the player up i.e same column but to the row above
    1. If the A key is pressed
        1. Move the player to the left i.e to the left column but same row
    1. If the S key is pressed
        1. Move the player down i.e same column but to the row below
    1. If the D key is pressed
        1. Move the player to the right i.e to the right column but same row

However, the player can only move in one of those directions if a platform exists and the platform is not infected.

    1. Check if the player wants to move to a row or column that is within the width and height of the two-dimensional array
        1. Check if the desired platform is not infected (ex. I created a class Platform and gave it a boolean property infected)
            1. Update the player's position to the new platform (i.e have variables that reference the current row and column of the platform the player is on and the platform itself)

The group of civilians follow wherever the player goes at some offset position.

    1. If the distance between a civilian's position and its offset position from the player is greater than 0 (i.e if the player has moved)
        1. Update the civilian's position each frame by linear interpolating between its current and desired position

![Player movement](/assets/gifs/cPlayerMovement.gif)

***Platform Selection***

Platforms are selected randomly and then become either infected or disinfected depending on its current state.

    1. If no platform is selected
        1. Generate a random number between 0 and the total number of platform rows (exclusive)
        2. Generate a random number between 0 and the total number of platform columns (exclusive)
        3. Declare the platform at that row and column as selected
        4. Switch the state of the selected platform (i.e infected to disinfected or vice versa) and its color
    2. If a platform is selected
        1. Start a timer
        2. If the timer is greater than the maximum time a platform can be selected for
            1. Change the state of the platform from selected to unselected (but do not change its color)

![Platform selection](/assets/gifs/cPlatformSelection.gif)

***Collision Detection***

A collision occurs if any of the civilians remain on a platform that has become infected.

**Note**: The X and Y coordinates of a platform represents the location of its upper left corner

    1. Create a function called collision that has two input parameters (reference to a civilian, reference to a platform)
        1. If the X coordinate of the civilian is within the range of the X coordinate of the platform's upper left and right corners
            1. If the Y position of the civilian is within tthe range of the Y coordinate of the platform's upper left and bottom left corners
                1. A collision is detected!
        2. Otherwise, there is no collision

    2. Call the collision function for each civilian after a platform's selection time has exceeded (i.e platform has become fully infected)
        1. If a collision was detected between a civilian and the platform, remove that civilian from the game (ex. I used the remove function in Processing)

![Collision detection](/assets/gifs/cCollisionDetection.gif)

**DEMO**

<iframe width="560" height="315" src="https://www.youtube.com/embed/S6nCfa1R5og" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>