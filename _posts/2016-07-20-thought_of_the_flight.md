---
layout: post
section-type: post
title: Thought of the flight
tags: [ 'Mesa', 'GSoC' ]
---
Hello

I'm in a plane to Paris so I think it's the good time to write a new post.

Since my last post, I keep coding the "soft" double precision floating point library in GLSL.
(My code is available on [my GitHub](https://github.com/Hopetech/libSoftFloat). Please, don't hesitate to review it !)
I worked on mul\_fp64, eq\_fp64, le\_fp64, lt\_fp64, add\_fp64 and fp64-to-fp32-conversion. But I probably did a silly thing with signed/unsigned.
Once all of this functions finished, I will create recip\_fp64 and rsqrt\_fp64.

For a few days now, my computer crashes when I did not seem to find the problem so I decided to change my distro.
I choose to use Ubuntu 16.04LTS but I've got some troubles building Piglit.
It's give me an idea: to avoid this troubles, I can make a Docker file for Piglit developers.
Like this, newcomers could easily have a working environment without loosing some precious times.
If it's work properly and people are interested, I could make a Docker for Mesa developers.

Have a nice day,

Elie "[hopetech](https://github.com/Hopetech)" Tournier
