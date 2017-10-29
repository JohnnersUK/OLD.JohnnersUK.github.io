---
layout: post
title: "Getting things moving"
date: 2017-10-13
excerpt: "Locomotion at its finest"
tags:
- L-LPG
- Game 2
feature: http://innovationexcellence.com/wp-content/uploads/2016/11/organizational-alignment-roadmap-1366x805-1024x603.jpg
comments: true
---

# Code talk about snake
## Road map
So far I have played around in ASGE, gotten sprites to move, text to render etc. just getting the hang of things really. I have also drawn up a sketch of what I plan the first level to look like:
_insert image_ <br>
As well as a full layout of my games core psuedo code and other plans which I cant show for fear of plagiarism. <br>
By my next update, in a week, i hope to have the core of my game finished so I can start working on the stealth mechanics of my game. This includes the guards AI, prisoner spawns, level maps and their goals.
<br>The week after i'll add a game over screen, leaderboards and an options menu. That should leave me with 1 week to fix any bugs and polish of the mechanics. _finger crossed._

Its a pretty solid four week plan and if i stick to deadlines and everyhting goes smoothly I should have a finished game on time for the feedback session on the 8th.
## Moving the snake and body
So i've decided that it would be more accurate to have my snake moving in chunks, like the original snake game, so i have planned to have the snakes head update on a counter. The game should take the users input and then once the counter has reached a set number, move the snake in that direction by howerver many pixels the snakes sprite is (currently 64x64).

For the boddies I plan to store each boddies last position, and then in a chain move each snake into a target position, which will be the last position of the snake body before it. Like some sort of cascading conga line of boddy parts. The first body piece will obviously have no body before it so it will initiate the chain by moving into the heads last position.

## Collisions
After a couple of hours of searching ASGE's header files, I've come to the conclusion that there isn't a set bounding box collision function built into the engine, meaning I will need to make one myself, which shouldn't be to hard seeing as I created all the collisions manualy for my game 'Super Maths Game' back when i was doing A-level computing. <br>
In theory you just take the origin of the sprite and see if any objects are within the x and y size of the sprite (So for snake within 32 pixels either side of the origin), if so then add a snake body, go to game over etc...

### And thats all for now
Thats all i've really gotten so far, snake isn't a complicated game as such, which is why i've allocated only a week to get the core game down. Will update next week with more progress, snapshots etc.