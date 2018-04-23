---
layout: post
title: "Constructing a robot class"
date: 2018-03-30
excerpt: "A brief rundown"
tags:
- Robot Wars
- L-LPG
feature: http://www.razkun.com/images/ubot/Ubot_Sketches_Small.jpg
comments: true
---
# Imitation is the sincerest form of flattery
Seeing as we're ripping off XCOM we may as well try and steal as many mechanic’s whole sale so in this post we will explore the soldier unit in XCOM and how we can apply them to Robot wars.

## The stats
Units in XCOM have a lot of stats, here’s a quick rundown; <br>
<img src="http://4.bp.blogspot.com/-jcxeYQwxZxI/Vjy9vMSYG6I/AAAAAAAAHaY/GSEseApUBNo/s1600/ufo1.colonel.statistics.jpg">

- **Time Units:** Time units dictate how much you can do in a turn. Every action costs TU (Moving one tile on flat ground costs 4 TU, A snap shot costs 12). A soldier cannot take an action if it exceeds their remaining time units.
- **Stamina:** Stamina is like time units but for movement only, even though moving also uses time units, It's a little confusing. If a soldier moves, they lose the amount of TU it costs as well as half that amount in stamina. <br> If a soldier hasn't got enough stamina, regardless of time units, they cannot move. Like TU, stamina recovers every turn, however unlike TU (Which recover completely after every turn) only a small amount is regained. This limits a soldiers ability to run about, but not their ability to do anything else.
- **Health:** This is how many hit points a soldier has.
- Bravery: This effects a soldiers chance to panic or go berserk whenever they or a friendly unit takes damage or dies.
- **Reactions:** The chance for a unit to attack a spotted enemy on the enemies turn if you had enough TU's to shoot at the end of your last turn.
- **Firing accuracy:** A soldiers chance to hit.
- **Throwing accuracy:** Same as above but with throwables
- **Strength:** How much gear a  soldier can carry.

## So what to rip
Obviously our game doesn't need to be as complex as XCOM, considering it's 3v3 in a small arena, but it still needs a layer of complexity to keep players coming back.

Ultimately we decided to keep a mix of XCOM's stats and our own, in the end we came up with:

- Energy: Time units, just renamed
- Health: Hit point
- Armor: Modifies damage taken
- Accuracy: See accuracy
- Range: How far each robot can attack
- Damage: How much damage a robot can inflict
- Manoeuvre: Chance to dodge/counter attack

# Constructing the class
Aside from the stats, the robots need a bit more to become a working class.
First they needed a move function. This function would simply move them to a target destination over time by setting a velocity.

```C++
void Move(int targetPos[])
{
    if (x_pos > targetPos[1])
    {
        x_vel = -1;
    }
    else if (x_pos < targetPos[1])
    {
        x_vel = 1;
    }
    else
    {
        x_vel = 0;
    }

    x_pos += x_vel;
}
```
_Example code to move an object to a target x position over time._ <br>
## Atacking function
To get the robots fighting they need both an attack and onHit function.

The attack function will calculate the damage to send over. This will be worked out by thaking the robot weapon's damage value and then multiplying it by 10% of the players level. We then need to check if the attack hits, This will be done by randomizing a number between 1 and 100 and seeing if it is less than the robots accuracy%.

After we're sure the attack hits we can call the target robots onHit function which will roll again, this time against the manoeuver of the robot, to see if they dodge the shot. If the shot successfully lands, the robots armour value is negated from the damage and then applied to the enemies HP. Nothing too fancy.

Finally we need to calculate the hit direction in order to determine which way to rotate the robot and in what direction to play the attack animation. This is just mathsy stuff, using Atan2 and passing in the difference in x and y of the two robots we can get the angle between them in radians. This can be used directly to set both the weapon animation and robot angle.

```C++
#include <math.h>

float calculateAttackDirection(int enemy_x, int enemy_y)
{
    int diff_x = robot_x - enemy_x;
    int diff_y = robot_y - enemy_y;

    float angle = aTan2(diff_x, diff_y);

    return angle;
}
``` 
## Getting the components

{% capture images %} ../assets/img/weapon.png ../assets/img/body.png ../assets/img/wheel.png {% endcapture %} {% include gallery images=images caption="Preview of the robot components" cols=3 %}

The robot would also need a weapon, body and wheels. Each of these would be its own class with its own sprite and stats. This will eventually allow users to customize their robots using has a relationships and initialization through JSON files.

These components will have theor own stats that would effect the overall robots stats, broken down like this;

**Body**
- Health
- Armour

**Wheels**
- Energy
- Manoeuver

**Weapon**
- Range
- Damage
- Accuracy

We'll get to that later but as a quick rundown, this should do for now.

