---
layout: post
section-type: post
title: Last week of GSoC program 
category: tech
tags: [ 'Mesa', 'Floating point', 'GSoC' ]
---
Hi everyone,

It's the last week of the Google Summer of Code but not of my contribution to Mesa.
The purpose of this post is to present the project progress.
The list of my commits done during the GSoC are available at [https://github.com/Hopetech/libSoftFloat/commits/master?author=hopetech]

#1. Me:
For the people who don't know me, I'm Elie Tournier, and I finish in June my study in IT engineering at Télécom Physique in Strasbourg, France.
You can find me on [GitHub](https://github.com/Hopetech/) or on [LinkedIn](https://www.linkedin.com/in/elietournier).
I enjoy C++ and Image processing. I'm an open source enthusiast.


#2. The organisation:
During this GSoC, I worked on the Mesa project.

_Mesa is an open-source implementation of the OpenGL specification - a system for rendering interactive 3D graphics.
A variety of device drivers allows Mesa to be used in many different environments ranging from software emulation to complete hardware acceleration for modern GPUs.
Mesa ties into several other open-source projects: the Direct Rendering Infrastructure and X.org to provide OpenGL support to users of X on Linux, FreeBSD and other operating systems._
(source: [mesa](http://www.mesa3d.org/intro.html))


#3. My project:
GPUs natively support single precision, but only OpenGL 4.0 class GPUs have hardware support for double precision. The goal of this project is to implement a library of double precision operations in pure GLSL 1.30 for this GPU using bit twiddling operations and integer math. There are many library of software double precision floating point for devices that lack floating-point hardware. I should therefore translate one of this library (generally write in C) to pure GLSL 1.30.

The functions I have to implement are the following:
*Add.
*Negate.
*Absolute value.
*Multiply.
*Reciprocal.
*Convert to single precision.
*Convert from single precision.
*Eq.
*Le.
*Lt.
Nice to have:
*Rsqrt
*Log
*Exp


#4. Accomplishement:
The list of my commits are available at [https://github.com/Hopetech/libSoftFloat/commits/master?author=hopetech]

|Function|Advancement|Comment|Link|
|Add|100||[https://github.com/Hopetech/libSoftFloat/blob/master/add_fp64.shader_test]|
|Negate|100||[https://github.com/Hopetech/libSoftFloat/blob/master/neg_fp64.shader_test]|
|Abs|100||[https://github.com/Hopetech/libSoftFloat/blob/master/abs_fp64.shader_test]|
|Mul|50|Compiler OK but trouble with the algorithm|[https://github.com/Hopetech/libSoftFloat/blob/master/mul_fp64.shader_test]|
|Recip|0||[]|
|Convert to single precision|100||[https://github.com/Hopetech/libSoftFloat/blob/master/fp64-to-fp32-conversion.shader_test]|
|Convert from single precision|100||[https://github.com/Hopetech/libSoftFloat/blob/master/fp32-to-fp64-conversion.shader_test]|
|Eq|100||[https://github.com/Hopetech/libSoftFloat/blob/master/eq_fp64.shader_test]|
|Le|100||[https://github.com/Hopetech/libSoftFloat/blob/master/le_fp64.shader_test]|
|Lt|100||[https://github.com/Hopetech/libSoftFloat/blob/master/lt_fp64.shader_test]|
|Rsqrt|0|||
|Log|0|||
|Exp|0|||


#5. What's next?
I engage with Mesa to provide the librairy so I will finish it.
After that, I will continue to contribute to the project.
A stretch goal would be to use this library of functions to implement GL_ARB_gpu_shader_fp64 on all GPUs for which Mesa supports GLSL 1.30.


#6. Gain for me:
During this summer, I discovered a shading language call GLSL and I improved my knowledge about double precision floating point.
More over, I took some time to rice my working environment. Now, I'm using vim with pluggins as IDE and i3WM as WM.
I think this choice will help me in the future.


#7. Thanks:
I would like to thank all members of Mesa and particularly Ian Romanick, my mentor.
Of course, thank to the staff of GSoC.
THANKS GUYS !

Elie "[Hopetech](https://github.com/Hopetech)" Tournier
