---
layout: post
title: "Static memory allocation"
date: 2017-10-02
excerpt: "All things static."
tags:
- L-LPG
- Research Notes
feature: http://s3.amazonaws.com/digitaltrends-uploads-prod/2017/07/close-up-computer-ram.jpg
comments: true
---
## An introduction to static memory allocation
Static memory allocation is where a specific amount of system memory is allocated for a given variable during compilation/
At the beginning of an applications lifetime.
This includes global variables, static variables, constants and arrays with a fixed size.
This contrasts directly to dynamic memory allocation which is allocated during the runtime of the program,
and can be changed to adapt to the variable.

Static variables can be good because they don't require programmers to free up memory after use, therefore being free
from memory leaks, they are easy to implement as you don't have to mess around with pointers
and are also very manageable (Dynamic arrays can quickly get massively out of hand if there is no hard limit on their size)

### Key example
Arrays are a good example of static v dynamic memory allocation.
Normally you would set up an array with a given size, like this:
```C++
int playerScore[99]
```
This is an example of static allocation as the array will be allocated 100 units of memory when the program is initialized,
this can be alright if you know there will be exactly 100 player per game.
You can also use pointers to change the size of an array during runtime.
```C++
int* playerScore = NULL
//some code later
playerScore = new int[numOfPlayers-1]
```
During compilation this array wont be allocated any memory, but when the line is called during runtime the array will be
allocated an appropriate amount of memory, depending on the amount of players in the game in this example.

### Determining scope and lifetime
Usually the scope of a statically declared variable is global as local variables get allocated when their function is called,
the exclusion being static local variables, this means that their lifetime is the entire lifetime of the application.

### Objects and static memory
If a class has a static variable in its properties, all objects made from that class will share that same variable
instead of creating a new local variable. This can be useful for a number of applications such as a unified pool
(Like money or something) shared by all members.

Classes can also have static functions that can be used to change the static variables within a class without the need
to create a object to modify the variable.

This can have a variety of uses for updating all objects from a class in one fell swoop.

```C++
class Vehicle
{
private:
    static int torque = 1;

public:
    static int setTorque(int x);
}

int setTorque(x)
{
    Vehicle::torque = x;
}
```

The above code show how you could use static variables anf functions to change the value of torque for all vehicle objects without the need to create one first.

All of this information has been condensed into a powerpoint presentation you can view bellow

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vQAgt88gUVj_gQp0Yj1r2Bbm3pmkVLZm7LN0wOl60xxqzQAzlNQOqmj2UaXbKW2wp9D2hXyBmujMb7r/embed?start=false&loop=false&delayms=3000" frameborder="0" width="480" height="299" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

---

Modernescpp.com. (2017). Pros and Cons of the various Memory Allocation Strategies. [online] Available at: http://www.modernescpp.com/index.php/pros-and-cons-of-the-various-memory-management-strategies [Accessed 2 Oct. 2017].
