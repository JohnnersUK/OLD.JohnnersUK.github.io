---
layout: post
title: "Staging Problems"
date: 2017-10-30
excerpt: "A story of over ambitious planning"
tags:
- Game 2
- L-LPG
feature: http://www.listchallenges.com/f/lists/45595ec5-7e32-44fc-8b25-a5ca1d9424aa.jpg
comments: true
---

# Late and tardy
So this post is a week late with good explanation, i messed up.

In my last post I overconfidently stated that it should take me only a week to mock up a simple snake game, needless to say that didn't happen à la missing post. <br>
On the good side, this means I can share some code. On the bad side, i'm almost 2 weeks beind schedule so I've decided to dithch the stealth game idea and make some more minor adjustments to my snake game.

## Broken trails
Turns out getting the snake sements to follow each other was harder than I had anticipated. <br>
My psuedo code looked a little like this
```c++
targetPosition = snakeHead.position;
updateSnakeHead(); //Function to move the player
for (int x = 0; x < player.length; x++)
{
    lastPosition = snakeBody[x].position;
    snakeBody[x].position = targetPosition;
    targetPosition = lastPosition;
}
```
Seems simple enough, in a dry run it should go something like this:

_lets say the snake position is [1,1] and all 3 boddies are to the left. B for body, H for head, - for target_ -> B B B H <br>
[1] targetPosition = snakeBody[x].position [1,1] <br>
[2] updateSnakeHead() moves the snake head to [2,1] -> B B B - H <br>
[3] -enter the for loop- <br>
[4] lastPosition = snakeBody[0].position [0,1] <br>
[5] snakeBody[0].position = targetPosition [1,1] -> B B - B H <br>
[6] targetPosition = lastPosition [0,1] <br>
[4] lastPosition = snakeBody[1].position [-1,1] <br>
[5] snakeBody[1].position = targetPosition [0,1] -> B - B B H <br>
[6] targetPosition = lastPosition [-1,1] <br>
[4] lastPosition = snakeBody[2].position [-2,1] <br>
[5] snakeBody[1].position = targetPosition [-1,1] -> - B B B H <br>
[6] targetPosition = lastPosition [-2,1] <br>
[7] -exit for loop- <br>

However apparently not, I'm probably just being dumb, but this code just wouldn't work. So after many hours I found a new method, it uses more memory due to storing more variables however it actually work so atleast theres that

## What now then?
Now that he core game is done I have just over a week left, not a lot. So i'm ditching the stealth game idea and taking a more simple approach.

Bats are going to fly at the player in increasing numbers, and the player can destroy the bats by shooting them. The players ammo reserve will be as big as the snake trail and the player can reload by collecting another pickup.

Fingers crossed this idea will be simple enough to polish off by the end of the week, including a full scoreboard and a simple options menu (for adjusting the difficulty, snake speed etc.) The hand in is thursday next week so I'll update again on saturday and then after I've recived feedback.

