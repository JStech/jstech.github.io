---
layout: layout
title: Laser cut paper snowflakes
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/7OtPeIniaAA"
frameborder="0" allowfullscreen></iframe>

Our department holiday party was last night. To help decorate, I cut about 50
paper snowflakes . . . with a laser.

The idea began as a joke. The department admin sent an email to the social
committee asking for help preparing decorations for the party, including cutting
paper snowflakes. Since I work in a robotics lab, I first thought I would
suggest we teach [Baxter][bx] to cut them for us. Then I realized that there is
such a thing as a paper-cutting robot&mdash;it's called a laser cutter.

![A snowflake](/res/flake.jpg)

A quick search for laser cutters on campus turned up the [Integrated Teaching &
Learning Lab][itl], and after two quick training sessions, I had access to a
laser cutter. They told us that the laser cutters are not for personal projects,
but this was for the department, of course!

I also needed to design the snowflakes. Some internet searching turned up [this
Stack Exchange post][se], which was exactly what I needed: a cellular automaton
that generates beautiful random snowflakes. I learned some Tkinter and installed
a Python package to generate .dxf files (which is the format Corel Draw reads
and prints to the laser cutter). The programming was more challenging than I
expected&mdash;lots of careful geometry. Ultimately, the code shows the
snowflake's growth one step at a time as I hit the space bar, and outputs to a
.dxf file when I hit 's'. It also resets with 'r'. I quickly had saved dozens of
flakes that I felt were particularly attractive. My code is [on Github][gh].

![Laying out snowflakes for cut](/res/planning.jpg)

I cut the flakes out of cardstock. I was able to fit about 7 flakes on an 11x17
sheet, which cut in about 20 minutes. I stacked two or three sheets for each cut.
Unfortunately, it generated a lot of smoke, and the flakes smelled like burnt
paper and some were slightly browned. Thankfully, they were used as decorations
on black table cloths and under dim lighting, so they ultimately looked pretty
good. I'd like to experiment more with the laser cutter settings to reduce the
smell and discoloration, although at this point that will have to wait for next
year. I suppose until then, I'll be dreaming of a white Christmas.

![Cutting snowflakes](/res/cutting.jpg)

[bx]: http://www.rethinkrobotics.com/baxter/
[itl]: http://itll.colorado.edu/
[se]: http://mathematica.stackexchange.com/questions/39361/how-to-generate-a-random-snowflake
[gh]: https://github.com/JStech/snowflake-art
