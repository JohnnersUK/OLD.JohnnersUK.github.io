---
layout: post
title: "Directors and managers"
date: 2018-02-19
excerpt: "How to scene"
tags:
- Birdman’s Break-in
- GLD
feature: http://4.bp.blogspot.com/-uL3JKOm61Es/UPUbtPJaTxI/AAAAAAAAAB4/jXJ2RHhGIO4/s1600/ccdirector-hierarchy.png
comments: true
---

# Handling scenes
Enums and function pointers have been the bane of my life over this past week as I just can't figure out the best way of loading levels in my scene.
Enums are great but they require state machines with repeating code so large and tedious that they aren't an effective use of line space.

Function pointers work just as well and require less effort, work and repeat code but I can't for the life of my get them working in a practical scenario.

Ultimately, I have settled on using a small Enum to switch between the main menu, play, pause and exit state as it is small and concise enough not to worry about. However, with this smaller Enum comes more problems.

## Loading levels
Using one play state is good and all but it means I need another sub-system for handling the level that the player is playing, on top of the state machine that switches between playing and being in menu's. This sounds overly complicated but using one massive Enum produces code a little like this;

```C++
enum States
{
	MAIN,
	Level1,
    Level2,
    Level3,
    Level4,
    Etc...,
	GAMEOVER
};
extern std::atomic<States> current_state;

Switch (current_state)
{
case States::MAIN:
    ...
case States::Level1:
    ...
Case States::Level2:
    ...
Case States::Level3:
    ...
Case States::Level4:
    ...
etc... etc... etc...
Case States::GAMEOVER:
    ...
}
```
So instead I've decided upon finding a way of loading each level into a generic scene which will then be run, a little like this;

```C++
switch (current_state)
{
case States::MAIN:
	...
case States::PLAY:
	currentLevel->play();
case States::GAMEOVER:
	...
}
```

Whilst more efficient, still requires a separate class for each level to be created and initialized for each scene in the game... not great, especially as our game requires upwards of 12 scenes. So, I'm currently pondering the idea of having a universal game objects pool and using the scenes as blueprints for how to construct each level into one scene and load them in and out when needed. Like a blank canvas and instructions on how to paint them, rather than a series of unique paintings being swapped in and out.

I'm not sure if this idea is any better or if will even work so there’s that.

If you want more updates you can check out my team’s blogs over [here](https://jamiehogg.github.io/) and [here](https://liamhumphries.github.io/)
and as always, stay tuned for more exciting development ventures.



