---
layout: post
title: 'Coronavirus 101: Social Distance'
---

`Processing`
<!-- excerpt -->

**DESCRIPTION**

A strategy game where the player protects a group of civilians from the coronavirus by guiding them towards uninfected platforms for as long as possible.

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
        1. Check if the desired platform is not infected (ex. I created a class *Platform* and gave it a boolean property *infected*)
            1. Update the player's position to the new platform (i.e have variables that reference the current row and column of the player and the platform itself)

The group of civilians follow wherever the player goes at some offset position

    1. If the distance between a civilian's position and its offset position from the player is greater than 0 (i.e if the player has moved to a different platform)
        1. Gradually update the civilian's position toward its new position by linear interpolating between its current position and the mew position

    
    

***Platform Selection***

***Collision Detection***