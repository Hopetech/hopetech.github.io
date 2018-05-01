---
layout: post
section-type: post
title: GPU virtualization update
tags: [ 'Mesa', 'QEMU', 'Virglrenderer' ]
---
A few months ago, Robert Foss wrote a [blog post about virtualizing GPU Access](https://memcpy.io/virtualizing-gpu-access.html).
In his post, Robert explained the architecture of the GPU virtualization stack and,
how to build and run a VM with hardware acceleration.

If you are interested by the GPU virtualization topic, I suggest you to read Robert's post.

Today, I will discuss the major improvements which landed upstream during these pasts 3 months.

# TL;DR:
* QEMU can now use OpenGL ES acceleration.
* Virglrenderer is close to be OpenGL ES 2.0 compliant.
* We are still working on OpenGL ES 3.0.

For each component of the stack, I will explain the added modifications and our plan for the future.

# Virglrenderer
At Collabora, have been working as part of the upstream community to add new features and improve the code base.<br/>
Most of our work consisted to added more caps to support OpenGL ES 3.0 on OpenGL ES and to find some workaround for the missing OpenGL ES features.
For example, OpenGL ES does not support 1D texture so we have to use a 2D texture with one of the component set to 0.5.

On my system, Intel KabyLake with Mesa 18.0.1, I obtained the following results:<br/>
* Android OpenGL ES 2.0 CTS on OpenGL backend: 4 failures<br/>
* Android OpenGL ES 2.0 CTS on OpenGL ES backend: 4 failures<br/>
* Android OpenGL ES 3.0 CTS on OpenGL backend: 40 failures<br/>
* Android OpenGL ES 3.0 CTS on OpenGL ES backend: ~2400 failures<br/>

The OpenGL ES 2.0 CTS failures are driver related. Tests fail on my system but pass on r600.<br/>
The difference between OpenGL ES 3.0 results might seem scary but a single fix should take care of it.<br/>
These failures are due to the fact that we don't support reading back results from integer (as opposed to floating-point) rendering, so all the tests for integer formats fall.

# QEMU
## Status
We can, since [4867e47](https://git.qemu.org/?p=qemu.git;a=commitdiff;h=4867e47cb637c6f3549786f1be70793112f96713), create an OpenGL ES context in SDL2.
Thanks to this, we can now run a QEMU on a system that only supports OpenGL ES.

## Running QEMU on an OpenGL ES backend.
If you want to try it out, you can follow the guide from [Robert's blog](https://memcpy.io/virtualizing-gpu-access.html).
The only difference, is the command line to run the WM,
you just need to replace `-sdl,gl=on` by `-sdl,gl=es`.<br/>

So it will become:<br/>

```
qemu-system-x86_64 \
    -enable-kvm -M q35 -smp 2 -m 4G \
    -hda ubuntu.qcow2 \
    -net nic,model=virtio \
    -net user,hostfwd=tcp::2222-:22 \
    -vga virtio \
    -display sdl,gl=es
```

Others flags are also available:<br/>
`-sdl,gl=core` Force to create an OpenGL context.<br/>
`-sdl,gl=on` Try to create an OpenGL context and if it fails,
             we fallback and try to create an OpenGL ES context.<br/>
`-sdl,gl=off` Disable the hw acceleration.<br/>

# Continuous Integration
Tomeu Vizoso initiated an effort to create a CI for Virglrenderer.
The CI is host on Freedesktop.org but validation is limited.
We only check that we are able to compile virglrenderer and that the dist-check passes.<br/>
The code for the CI is available [here](https://gitlab.freedesktop.org/tomeu/virglrenderer/tree/ci-surfaceless).

# What's next?
* One of our long-term goals is to be compliant with the current OpenGL ES specification.
* We also want to improve the CI. We currently check that we are able to compile Virglrenderer and that the basic testsuite passes.
  The next step will be to run the Khronos Conformance Test Suite and/or Piglit.
  Virglrenderer is now being used in big projects so we need to make sure that new patches don't introduce any regressions.
* Security improvements. One of the main reasons to use containers is the process isolation.
  A bad implementation can cause leaks, give access to some unautorized components or even worse crash the host system and
  lose all the advantage of process isolation.
  One of the solution disscused with upstream is to use a memory safe programming language like Rust.
  We are still in discution.<br/>
  See [this thread](https://lists.freedesktop.org/archives/virglrenderer-devel/2018-April/000394.html)
* Performance and debugging improvements.

# Thanks
This post has been a part of work undertaken by my employer [Collabora](https://www.collabora.com).

Elie "[hopetech](https://github.com/Hopetech)" Tournier
