---
layout: post
title: Designing A 12V To 5V 2A Flybuck Converter
---

As mentioned in my Fan and RGB controller blogs, I have run into power issues on the 5V rail of my Arduino. When trying to run an RGB strip directly of the Arduino's power causes the device to shutdown due to too much current draw. The easiest solution for this is to provide a second source of 5V power. And there are several options out there to obtain 5V power. A cheap flybuck converter off amazon or a 5V power supply are both reasonable options. However, I want to learn and explore areas of embedded systems that I haven't before.

So my solution to this is to spend far too much time and money designing and building my own PCB to supply enough power to run the RGB strip, while still allowing me to run to a 12V fan and the Arduino. So with the disclaimer that this was not a smart idea, and that I have never done any sort of PCB design before, here is my plan and the results so far.

# Plan:

With no prior experience in PCB design and only a basic understanding of power circuits, buck converters and related topics, my first step was to look at some guides and alternative designs. Ultimately I settled on using the guide linked below as the basis for my own work as it was easy to follow with details on where they got their information, but different enough to my own goals that I would still have to do my own work. 

https://www.instructables.com/DIY-High-Efficiency-5V-Output-Buck-Converter/ 

With a guide sorted, I started looking into what buck converter I would use as the basis of my design. I knew I wanted 5V output, capable of at least 2A, and with a 12V input. However, I also had some bonus criteria too. I wanted an adjustable output between 3V and 12V so I could bring the design forward in the future. And similarly I wanted an input range between 12V and 48V in case I decided to upgrade my input powersupply for my power hungry projects. 

The first buck convert I found that fit my main requirements was the LM2592HVSX-5.0/NOPBCT-ND. It is fixed to a 5V output, but a 3.3V and an adjustable version exist so they could be swapped in to fit my bonus criteria with some minor design changes. Furthermore, it supports inputs between 6V and 60V which encompases my other bonus critera. However, the component is quite expensive at £4 per unit, and the form factor was quite awkward. 

Fortunately, there is a more recent model which seems to resolve all my complaints. The LMR36520ADDAR from Texas Instruments has the same input voltage range, and an adjustable output voltage range between 1V and up to 60V depending on the input voltage. It has an output current of up to 2A, fitting my current requirements. The form factor is also more appropriate, and the price is less than half of the previous model. Furthermore, Texas Instruments offers pin compatiable buck converters with high current ratings and other specifications, meaning the PCB I design will have a high degree of versatility. 

With the buck converter chosen, I began looking through the documentation for guides on how to use it. Very fortunately for me, the documentation provides information on exactly how to set the buck converter circuitry to receive a desired output, with resistor values, recommended inductor values and capacitor values. There is also an evaluation board with all the itemised components used to make it included in the documentation as well, along with a reference PCB.

![LMR3650 Reference PCB](https://github.com/Billy5691-2/Billy5691-2.github.io/blob/master/images/Reference_PCB.jpg?raw=true)

My next step was to then select components and design a board. Component selection was easy thanks to the evaluation board containing all the components I would need, except for an inductor which was no longer available on Digikey. For the resistors, I maintained the same series but went for resistances which fitted my use case better. 

And then I moved onto design, where I used the EasyEDA web interface to create a circuit schematic, convert it to a PCB schematic and produce a gerber file. 

# Design:

![PCB Top](https://github.com/Billy5691-2/Billy5691-2.github.io/blob/master/images/PCB_Top.jpg?raw=true)

![PCB Bottom](https://github.com/Billy5691-2/Billy5691-2.github.io/blob/master/images/PCB_Bottom.jpg?raw=true)

Creating the circuit schematic was relatively easy as I just had to connect the correct components together, with most components being bidirectional, while following the LMR3650 pin out documentation. 

The more complex part of the design is the actual PCB layout. I chose to use a 2 layer design instead of the recommended 4 layer design from the documentation as I am not expecting to fully stress the power delivery continously, and I wanted to reduce costs. Furthermore, I will make up for the reduced PCB mass by adding small heatsinks and providing active airflow via a fan. 

But other than that change, and the addition of connector pins, a barrel jack and a bulk input capacitor, I followed the design from the reference PCB as best I could. I add also add extra pads for more resistors in case I wanted to change the output voltage in future. 

With the initial design sorted, I spent some time making alterations the layout, adding vias and changing the size of the power planes. Due to the high amount of waste heat produced during power conversions, I wanted to have a large ground plane as they recommened. So a majority of the top layer, and almost all of the bottom layer were dedicated to grounding for heat dissipation, with a large number of spread out vias to allow heat to spread evenly. 

However, I also wanted to ensure the VIN and VOUT planes also had a decent amount of space so they they didn't have too much resistance, producing more heat. I also chose to have 2 VIN connectors instead of just one, as my expected use case of this design is to power a fan and an Arduino with 12V from the VIN plane, so I wanted to spread the current out between the two pins instead of using a daugther board to split the power. 

Lastly, I will be using 2oz copper for both layers instead of 1oz copper for the improved heat dissipation with the trade off of increased cost. 

# Components:
Here are my exact component choices:

Buck: 
Texas Indstruments - LMR36520ADDAR

Inductor:
TDK Corporation -SPM10065VT-100M-D
10uH, 8.1A


CIN1, CIN2:
TDK Corporation - CGA6M3X7S2A475K200AB
4.7uF, 100V

CVcc:
TDK Corporation - C1608X5R1E105K080AC
1uF, 25V

CVBoot:
KYOCERA AVS - KGM15BR71E104KT
0.1uF, 25V

CO1, CO2, CO3:
Samsung Electro Mechanics - CL32A226KAJNNNE
22uF, 25V

CHF1:
Murata Electronics - GRM21AR72A224KAC5L
0.22uF, 100V

CINB:
Panasonic Electronic Components - EEE-TG2A220UP
22uF, 100V

RFBT:
YAGEO - RC0603FR-07100KL
24.9K Ohm

RFBT (3.3V Recommended Alternative): 
YAGEO - RC0603FR-0746K4L
46.4k Ohm

RFBB:
YAGEO - RC0603FR-0724K9L
100K Ohm

Barrel Jack:
Kycon - KLDX-0202-BC
2.5mm-5.5mm, Positive Center

# Results:
I have yet to order the components or PCB, but I will update this section when I have recieved both and had a chance to test them. 



