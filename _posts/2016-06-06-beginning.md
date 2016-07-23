---
layout: post
section-type: post
title: The first 2 weeks of coding period
category: tech
tags: [ 'Mesa', 'Piglit', 'GSoC' ]
---

Hello everyone,

**TL;DR:**
**As a reminder, the goal of my GSoC subject is to implement a software double precision floating point library in pure GLSL 1.30.**
**During this period I was able to define more precisely the different stages of the project as well as the development tools to use. This is "shader\_runner" a Piglit component, which allows to execute the GLSL code.**
**I start by implementing the "easiest" functions like float\_to\_ double conversion, double\_to\_float conversion and absolute.**

**However, I have fallen behind because of my exams but also job interviews.**

**I met some difficulties with Piglit because of the lack of documentation.**

Today I decided to tell you a story, one of my first few weeks of coding for the GSoC program.

Once upon a time...
The story began the 22th of April 2016 when I see my name on the GSoC page. I was like a child who received a new toy.
I grabbed my laptop and begun to customized my workspace. I chose to use vim for this project. It seemed to me that it was the right time to improve my knoweledge about this tools. If like me, you want to begin with vim, I advise you to watch [this video](https://www.youtube.com/watch?v=_NUO4JEtkDw). 
With vim, I use [Pathogen](https://github.com/tpope/vim-pathogen) for manage my runtimepath, [Syntastic](https://github.com/scrooloose/syntastic) for syntax checking, [vim-markdown](https://github.com/tpope/vim-markdown) for edit markdown files with vim and [vim-glsl](https://github.com/tikhomirov/vim-glsl) customed by myself for enable hightlight in shader_test files.
My dot files can be found on [Github](https://github.com/Hopetech/dotFiles).

Let's speak about the project.
One of the first thing I wanted to clarify was how can I test my code. Ian advise me to use [Piglit](https://piglit.freedesktop.org/), more precisely, "shader_runner". So we decided to use this tool to dev and test each functions of the library.
After the development, I will have to integrate the library into the Mesa project. But we doesn't speak about it for the moment: first things first.

The second thing to know was how to store our 64 bits. We will use two unsigned integer in a uvec2. Unsigned integer allow us to use bit twiddling operations.

So I began by implementing float\_to\_double. We wanted to convert a [simple precision](https://en.wikipedia.org/wiki/Single-precision_floating-point_format) to a [double precision](https://en.wikipedia.org/wiki/Double-precision_floating-point_format).
Technically, we just had to extract the 3 parts of the number: the sign bit, the exponent and the fraction of the float. Then add each part in the right place of the double. It's easy to fit a 32 bit in a 64. But in the other way, it's more difficult.
The second function I had code is negate. For that, we toggled the sign bit.
The last function on which I worked is the absolute value. We just had to clean the sign bit to 1 by apply a mask on our double.

During that time, I met some difficulties:
I struggled to integrate my function in Piglit and to run shader\_runner because I don't found so much documentation about it. So I couldn't test my code.
More over, I have fallen behind because of my exams but also job interviews.

**To summerize, I realize 3 functions (float\_to\_double, negate and absolute) but I still have to check my code by the community and to understand how to properly use piglit.**

Have a nice day of coding!
Elie "[Hopetech](https://github.com/Hopetech)" Tournier
