---
layout: post
title: "Static memory allocation"
date: 2017-10-02
excerpt: "All things static."
tags: [L-LPG]
feature: http://s3.amazonaws.com/digitaltrends-uploads-prod/2017/07/close-up-computer-ram.jpg
comments: true
---
## An introduction to static memory allocation
Static memory allocation is where memory is allocated during compilation, before the program is executed.
This includes global variables, constants and arrays with a fixed size. This contrasts directly to dynamic
memory allocation which is where memory is allocated during the runtime of the program an can change
to adapt to the variable.

### Key example
Arrays are a good example of static v dynamic memory allocation;
Normally you would set up an array with a given size, like this:
```C++
int numArray[100]
```
This is an example of static allocation as the array will be allocated 100 units of memory when the program is initialized,
however you can also use pointers to change the size of an array during runtime.
```C++
int* numArray
//some code later
numArray = new int[20]
```
During compilation this array wont be allocated any memory, but when the line is called during runtime the array will be
allocated 20 units of memory

### Determining scope and lifetime
Usually the scope of a statically declared variable is global as local variables get allocated when their function is called,
the exclusion being static local variables, this means that their lifetime is the entire lifetime of the application
