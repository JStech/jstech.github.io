---
layout: comments
title: Just a Flashlight
published: false
---

A simple flashlight app was one of the first things I downloaded when I got a
smartphone. The thing has an LED, why shouldn't have a simple way to turn it on
and off? Of course, the app came with ads.

I've made a few false starts at learning Android. I decided that I should be
able to handle a flashlight app---after all, it can't be that hard to turn a
light on and off, right? And then I don't have to sell anyone my attention, even
for the fraction of a second it takes to ignore the ad completely.

Unfortunately, it hasn't proven easy. Even after I gave up on using the new
`camera2` interface, I was still adrift in a sea of Java. I found several
examples online, and tried working from them to various degrees. I'm not sure if
they were out of date, or they were doing things in a way that doesn't work with
my phone, or if my customizations were to blame.

Finally, I pared my code down to closely mimic one example, and I got it to
work!

. . . mostly. It doesn't release the camera, and misbehaves when the phone switches
between landscape and portrait. I hope most of these problems will be fixed by
moving code off the main thread. I'll also make it release the camera when the
light is turned off, instead of in `onDestroy()`. But I still feel accomplished
whenever I click the light on and off.

My code is [on Github][gh].

[gh]: https://github.com/JStech/just-a-flashlight
