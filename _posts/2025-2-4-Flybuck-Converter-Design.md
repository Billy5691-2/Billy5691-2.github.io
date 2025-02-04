---
layout: post
title: Designing A 12V To 5V 2A Flybuck Converter
---

As mentioned in my Fan and RGB controller blogs, I have run into power issues on the 5V rail of my Arduino. When trying to run an RGB strip directly of the Arduino's power causes the device to shutdown due to too much current draw. The easiest solution for this is to provide a second source of 5V power. And there are several options out there to obtain 5V power. A cheap flybuck converter off amazon or a 5V power supply are both reasonable options. However, I want to learn and explore areas of embedded systems that I haven't before.

So my solution to this is to spend far too much time and money designing and building my own PCB to supply enough power to run the RGB strip, while still allowing me to run to a 12V fan and the Arduino. So with the disclaimer that this was not a smart idea, and that I have never done any sort of PCB design before, here is my plan and the results so far.

# Plan:
