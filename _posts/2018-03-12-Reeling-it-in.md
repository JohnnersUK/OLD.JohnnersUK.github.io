---
layout: post
title: "Reeling it in"
date: 2018-03-05
excerpt: "Polishing break-in"
tags:
- Birdman’s Break-in
- GLD
feature: http://opargo.com/wp-content/uploads/2016/09/AdobeStock_103060701-1140x560.jpeg
comments: true
---
# Birdman speedrun
<div style='position:relative;padding-bottom:57%'><iframe src='https://gfycat.com/ifr/LavishBigheartedJapanesebeetle' frameborder='0' scrolling='no' width='100%' height='100%' style='position:absolute;top:0;left:0;' allowfullscreen></iframe></div>

## Rounding things off
So after the scene manager and data driven objects were created, all that’s was left to do was create the scenes for the scene manager to... manage. Sticking with the original plan we managed to create 4 scenes that all tied together to make a short puzzle that would show off the tech that was there. These 4 scenes included the alleyway, back street, corner shop and theatre entrance which can be seen bellow;

{% capture images %} ../assets/img/birdman1.png ../assets/img/birdman2.png ../assets/img/birdman3.png ../assets/img/birdman4.png {% endcapture %} {% include gallery images=images caption="Birdman scenes" cols=2 %}

Scenes in birdman were relatively simple. They contained a vector af game objects that would polymorphically store the NPC’s and items, birdman and a sprite for the background. 

This meant that scenes could be designed easily and rapidly, making future expansion of the game relatively simple.

## Squashing the bugs
There weren’t many bugs throughout the development of the game due to the simplicity of the code base, however a few crept into the final project.

- The delta timed timer doesn’t work unless the game is running at exactly 30 frames per second. This makes me thing the clock wasn't delta timed correctly but that's something I didn't work on, something we only discovered on the day of the hand in. 
- Incorrect hitboxes on certain NPC's due to human error making the text files. This could be fixed by automatically detecting the sprites dims instead of inputting them.
- The player isn't delta timed at all meaning you can zoom around the map real fast with your GTX titan
- The next scene buttons can be accessed from across the screen (Easy fix)
- The player appears on the incorrect side of the screen when transitioning to the left (Also an easy fix)

These were all relatively small bugs so we weren’t worried about their impact on the final grade

## The result
A solid pass, yet again there were some errors in the code base that held us back but the overall gameplay experience (Or at least what there was of it) was praised highly. We were told the game felt relatively polished for what was there, but there needed to be more. 
All fair comments, the game was 30 seconds long after all.

Thank you all for joining me on this adventure and as always, stay tuned for more!