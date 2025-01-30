---
layout: post
title: Fan and RGB Controller - Part 2
---

In this blog I will go into further detail my plans for step 1 for creating an Fan and RGB Controller, and when I will move onto step 2.

## Hardware:

My first challenge in this project was finding an appropriate board to work with. I initially have a few requirements for the board:
- PWM pins for controlling the fan.
- Analog pins for reading the thermistor data.
- 5V output for powering RGB.
- 12V output or passthrough for powering the fan.
- Optional: Wifi for future projects
- A strong ecosystem to work with for future projects or if I run into issues.

With those requirements set, I began looking. My immediate focus was on Ardunio because of the large ecosystem along with a large portion of their options providing functionality I need. So from there I just had to establish which board I would purchase.

Initially, I was leaning towards the Ardunio Nano as it had all the features I required. However, power would have to be provided through input pins. Furthermore, 12V was at the limit of its accepted input voltage and I worried about overstressing the power delivery circuitry. So I kept looking, leaving this as a back up. 

The next board I looked at was the Ardunio Uno 4. Like the Nano, this had all the same functionality, but with a few extras. Firstly, it could accept up to 24V input instead of 12. Secondly, it had a barrel jack connector for power, on top of the VIn pin and USB connector. Thirdly, there was an option with an inbuilt WiFi chip and a matrix of LEDS, both of which could be used in future projects. All while only slightly more expensive than the Arduino Nano. This became my primary pick.

I did look through some of the more high end models of Arduino, but found they provided no extra functionality to justify the higher price for my project. 

With the board sorted, I also purchased a 12V 2A barrel jack power supply to power the board and the fan I would be running my tests with. While not ideal as there was a risk of overstressing the components of the Arduino from high power draw, I decided to would be an acceptable risk for the testing stage, and I would avoid drawing too much power through the board to avoid damage. 

For a test fan, I decided to use a basic 120mm PWM fan I had spare from previous computer builds. 

For the thermistor, I will ultimately use an in waterloop thermistor with a preattached fitting, so for now I will use a basic thermistor from a hobby electronics kit, along with a breadboard and resistors. 

## Software:

For software, I will be using what Arduino offers as I am using an Arduino board. 

I plan on first implementing basic PWN control for the fan. This will help me familairse myself with the software and PWM control. I will then move onto temperature reading, which I do not expect to be much of a challenge. After which I will combine PWM control of the fan with the temperature reading to have the temperature affect the PWM speed. And lastly, I will work on making the fan react in a manner appropriate to temperature changes. This means leaving time for fans to ramp up and down at a rate that won't create awful noise, and avoiding unnecessary changes in speed for brief temperature swings. 






