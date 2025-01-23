---
layout: post
title: Fan and RGB Controller - Part 1
---


In this blog I will lay out the goals and steps I will take to one day create my own fan and addressable RGB controller for my water cooled gaming PC, as well as my motivations for my project. 

There is no guarantee I will achieve a satisfactory end result from this project, but I hope I will learn plenty from the attempt and the challenges I face. 

## Motivation:

I currently make use of mostly Corsair components with an ASUS motherboard. This is fortunate as ASUS has integration with Corsair’s ICUE software so I can control fan curves and RGB from one place. However, Corsair’s ICUE software has several issues:

Firstly, a performance impact which can have up to a 10% drop in FPS in some games. This is caused by the software constantly polling temperatures from the CPU, GPU and other components' internal sensors. However, as my computer is watercooled, the temperature of individual components is irrelevant beyond making sure nothing has gone wrong. What matters is the temperature of the water, which is measured by a thermistor in the water loop itself. 

Secondly, Corsair’s ICUE software can cause sleep bugs and other issues with my system. Putting my PC to sleep will cause issues with ICUE upon waking. My previous install of windows 10 also had a bug where my monitors would never turn off due to ICUE. Fortunately this was fixed with my most recent install, but I am hesitant to update ICUE in case the ASUS integration breaks or new bugs appear. 

For the above reasons, I would like to stop using ICUE if possible. However, I currently require ICUE to control fan speeds and my RGB. Alternative software such as Signal RGB exists, however I would prefer to go for a mostly hardware solution as this seems like a fun challenge for a minor problem with no desperate need to be solved. 




## Goals:

The end goal of this project will be to create a majority-hardware solution for fan and rgb control. This will require a PCB with fan and rgb ports, as well as controller chip and storage, and a way to change profiles on the controller and power the board.

The hope of this solution is that there will be no performance impact on my system as the controller will be able to run independently from the rest of the computer, only needing a connection when changes to fan curves or rgb designs are made. All temperature readings could be done directly from the board with a thermistor in the water loop, and fan curves and rgb designs would be saved on device so they could be loaded when power is provided. 




## Initial Solutions:

Some parts of the final solution are obvious now. Molex or sata can be used to power the final board. Thermistors which fit seamlessly into a waterloop already exist. I believe Corsair, despite using a proprietary standard connector, uses a standard ARGB protocol. 





## Steps:

I will be breaking this project into smaller, more manageable steps in hopes of making the end goal easier to reach.

Step 1 will be to use an Arduino Nano to control one fan with a thermistor. This will allow me to understand fan curves, fan ramp up and down, as well as temperature inputs. All while avoiding more complicated issues. I have researched this and know it is possible.

Step 2 will be to use the Arduino Nano to control an ARGB strip. This will give me a chance to learn about the ARGB signal protocols and programming my own interesting patterns. I have not researched this so far, but believe it will be possible.

Step 3 will be to incorporate step 1 and 2 into the same program.

Step 4 and beyond will look at creating the required PCB along with the necessary components.

I will create a new blog at the end step 3, outlining progress thus far and elaborate more on the future steps. 





## Stretch goals:

If this project ends up being easier than intended, I will look at adding wifi capabilities so the fan curves and RGB patterns can be altered remotely, possibly via a mobile app.
