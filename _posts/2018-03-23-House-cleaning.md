---
layout: post
title: "House cleaning"
date: 2018-03-12
excerpt: "Preparation is key"
tags:
- Robot Wars
- L-LPG
feature: https://www.hungryshredder.co.uk/wp-content/uploads/2017/10/Paperwork.jpg
comments: true
---

# New group, new code
Before we can get started coding robot wars we decided that we should pick apart systems from older projects to save some time coding.
This was a tedious process but necessary as the scope of this project was big and the time we had small. Ideally by the end of it all we would have the underlying systems to build our game in place, minus the networking.

The systems I would have to pull were chosen because nobody else had implemented them as of yet. That meant I was going to have to pull:
- the user input (Specifically mouse)
- Audio support
- Animated sprites
- a more complicated data driven object class.

## Mouse input
All inputs are handled through the engine so the code to get them working is specialized and not useful to display, doesn’t stop me talking about it though so I will.

ASGE uses call back functions and input handlers to poll for the user’s inputs. Listening for and then taking this data and storing it in a variable is essential as this then allows us to process these inputs further.

Using these functions, I can extract what button the user has pressed, what action they performed (Pressed, released) as well as any modifiers (Such as ctrl, alt etc.).

This data is tied into their own Enum classes which can be accessed through the game, independent from the scene manager:
```C++
enum ButtonLabel
{
    LEFT,
    RIGHT,
    MIDDLE
}
atomic<ButtonLabel> button_label;

enum ButtonAction
{
    PRESSED,
    RELEASED
}
atomic<ButtonAction> button_action
```
*Example enums for the mouse states*

These enum's are then checked and then used within each scene in a processInputs() function. This is a generic function that is customized per scene but could look something like this:
```C++
void processInputs()
{
    switch (button_label)
    {
    Case ButtonLabel::LEFT:
        player.moveTo(cursorPosition);
    }
}
```
*Simple function that moves the player to the cursors position on click*

## Animated sprites
I've already covered animated sprites for dinky little dino so here I'll just go over some changes that I made to the base code.
### Play, Pause and Stop functions
```C++
void Play()
{
    is_playing = true;
}

void Pause()
{
    is_playing = false;
}

void Stop()
{
    is_playing = false;
    current_frame = 0;
}
```
Simple functions to give more control over the playback of the sprite
### Framerate and current frame
```C++
void Update()
{
    count += Time.DeltaTime;

    if (count > current_framerate)
    {
        current_frame ++;
    }
}

void setFrameRate(int new_framerate)
{
    current_framerate = new_framerate;
}
```
Allowing for custom framerates means that we can now tweak how fast animations play and completely decouple them from the games main update loop, a problem that plagued dinky little dino as the player controller was forced to update in accordance to the animations frame rate (Causing microscopic input lag and a character controller that moved differently from the game world, it was a weird feeling)

```C++
void setCurrentFrame(new_frame)
{
    current_frame = new_frame;
}
```
This allows frame skipping as well as frame delaying, a useful visual feedback technique that can be used for a plethora of things like freezing the animation for a split second when the player is hit.

### Audio support
**Now featuring irrklang!** <br>
iirklang is a low level c++ library that allows for simple audio playback with surprisingly deep customization. <br>
All you need to do is set up the audio engine:
```C++
using namespace irrklang;
audio_engine.reset(createIrrKlangDevice());
if (!audio_engine)
{
    // error starting audio engine
    return false;
}   
```
Add some sounds:
```C++
Music = audio_engine->addSoundSourceFromFile("../../Resources/Sound/Music/BGMusic.wav");
Music->setDefaultVolume(0.25f);
```
And the play!
```C++
audio_engine->play2D(Music, true);
```
Real easy stuff, for more sound just add more sources

### JSON
**Also featuring JSON!**<br>
Not much to write here, I've moved on from .txt files and have started using JSON files for data driven objects. More info can be found in the data driving section of the birdman project.

## And that’s all for now!
Took about 2 days to get all of this implemented but it's done, for now.
Stay tuned for future updates and as always, thanks for reading.