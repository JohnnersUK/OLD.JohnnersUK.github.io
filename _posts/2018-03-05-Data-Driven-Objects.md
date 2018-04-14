---
layout: post
title: "Making use of them Buses"
date: 2018-03-05
excerpt: "Information highway"
tags:
- Birdman’s Break-in
- GLD
feature: http://opargo.com/wp-content/uploads/2016/09/AdobeStock_103060701-1140x560.jpeg
comments: true
---
# Data driven objects
So my personal coding challenge this week was to try and mess around with type classes and has-a relationships with the final goal of data driving the NPC's and items in my upcoming game, Birdman’s break-in. 

## What?
For those who don't know, Data driving objects is where you initialize an object by reading in from data files (.txt, .ini or .json most commonly). 
## Why?
This has 2 benefits;
First, objects that are data driven can be changed without hard code. Say you design a generic system for NPC's in a game that would be passed onto the designers and artists to fill a game with characters. By data driving the objects, the designers don't need to know how to code, they just edit a text file and boom, more NPC's.

And secondly, balancing a game becomes so much easier when you can just open a text file and change some damage values without the need to rebuild the entire game. Whilst not fully applicable here, a game like say... the Witcher 3, would take quite some time to compile. And over time, this can really speed up the development process.

<img scr="../assets/img/birdman1.png">

## How?
Data driving the objects in birdman’s break-in proved to be real easy.
<img scr="http://i0.kym-cdn.com/entries/icons/original/000/021/807/4d7.png">

Both the NPC's and Items would have an init function that would be called on declaration and passed the directory of the item's text file (E.g. pen.txt).
This text file would contain a directory for a sprite, name, description and a few other things related to trading and combining.

```C++
pen.txt
Name: Pen
Sprite: Pen.png
Description: A simple pen
Combination: Nothing
```

The init function would then find and open the file and then initialize all of the objects various variables. Bish bash bosh and we have ourselves a data driven experience.

```C++
if (myFile.open())
{
    if (myFile >> name >> sprite >> description >> combination)
    {
        return true;
    }
}
```

<img scr="../assets/img/birdman2.png">

So now say I wanted to change the flow of the game; say I wanted the drain to give you a token, not the homeless man. I'm just one small line away from doing so, no recompiling, no hassle.

# The state of things
Sorry for the lack of posts recently, to keep it brief, Uni's been a real stressor in my life so far. Know how I linked my team in the last post? Notice how they're not linked in this one? Yeah, I'll leave it at that.

Anyways, hope you enjoyed this short snippet into my learning, and as always, stay tuned for more posts.