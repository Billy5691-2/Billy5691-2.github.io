---
layout: post
title: My Hex Strategy Battler Project
---

As a side project to keep my programming skills fresh, I often make little games. However, this time I have gone for something slightly larger in scope. 

Based on a mini-game in Horizon: Forbidden West, I am creating a turn-based strategy game built on a hexagon grid, where two players battle some form of units until one side has been eliminated. 

My initial plan is create this game in Python using PyGame for the UI. This is because I am familar with both. However, I may choose to recreate this one day in C or C++, with the intention of expanding from the basic battler into a more complicated and complete game. There is the potential for creating a roguelite or roguelike deckbuilding game with procedural generation to create routes and potential battles. However, this is a long term option with the main goal of the current goal being to create a simple battler, first between 2 players, and then between an AI and the player.

I have prior experience creating AIs from my Master's degree, so it would be fun to use those skills to make a new AI for a video game of my creation. Especially as the goal of this AI would be different from my Master's project. My master's project was trying to show the feasibility of creating an AI for the videogame Puzzinc. However, this game is a completely different genre which means the AI will be very different. And I will also ideally make multiple difficulty levels so that a player could choose how hard the AI is, which will be a new challenge entirely. 

## Problems:

My two biggest obstacles I can forsee so far are hexgrids and AI.

Hex grids will be an issue as they are more complicated than a simple square grid, which could be stored in a 2D array. However, after being unable to come up with a clear solution myself, I found a document which outlines all the functions I need to be able to work with hex grids for this game. https://www.redblobgames.com/grids/hexagons/. Furthermore, they have the code prewritten if I ever chose to move onto the more complete version of the game in C++. 

The next obstacle I forsee is the AI as I have never tried to create an AI for a game like this. However, I look forward to the challenge, and I believe with some effort and research I will be able to create something serviceable when I reach this stage. I may discuss this more when I reach the point where an AI is needed, but for now I will just focus on making the 2 player game but with modularity to add an AI player when needed. 
