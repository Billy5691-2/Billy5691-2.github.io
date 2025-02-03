---
layout: post
title: Fan And RGB Controller - Part 3
---
With the Arduino arriving in the post a few days ago, I can now discuss my progress, thoughts and future plans in more depth. 

## Progress:

Within a day of getting my hands on the Arduino, I was able to achieve most of my desired goals for stage 1. 

![Arduino connected to fan](https://github.com/Billy5691-2/Billy5691-2.github.io/blob/main/images/Arduino_Fan_Thermistor_1.jpg?raw=true)

![Arduino thermsitor circuit](https://github.com/Billy5691-2/Billy5691-2.github.io/blob/main/images/Arduino_Fan_Thermistor_2.jpg?raw=true)

I successfully implemented a thermistor circuit and attached the fan to the Arduino Uno 4. I was then able to implement a program to read the voltage from the thermistor circuit and convert it into a temperature. I was also able to implement PWM control over the fan, and combine the two functions to have a temperature controlled fan. 

From there, I implemented a rolling average temperature based on the previous measurements to smooth sudden temperature changes and reduce the rate of fan ramp. 

Despite only having a small amount of experience with C++ and no experience with arduino, I found I was able to quickly pick up both and neither provided significant issues. 

## Challenges:

I did run into a few issues while implementing the above program though. 

PWM control fro the Arduino Uno 4 is different to some of the other Arduino models, such as the Nano. This caused problems as the guides used to learn how PWM works were wrong. However, I did manage to figure out the correct commands eventually and found that the Uno R4 is actually far easier to control PWM than some of its sister products. 

The rolling temperature program also caused some issues. Initially I had a list of length X, and I would update item 0 in the list after propogating all the values up by 1 index point and deleting the last value. However, there was an bug where a value which I needed to assign twice would erase itself after the first assignment which meant the second one would fail.

I managed to work around the bug by using multiple assignments, however, in the process I discovered a better solution to my problem. Instead of propogating previous temperatures through the list, I instead track an index which rolls over at the end of the list and is used to update values in the list. This makes the program marginally faster as less calculations are required per loop. 

![Rolling Temperature Implementaion:](https://github.com/Billy5691-2/Billy5691-2.github.io/blob/main/images/Rolling_Temp_Code.jpg?raw=true)

My final challenge is one of physics and is not directly related to the above challenge. The Uno R4 operates at 5V with a buck converter capable of producting 1A of current. To provide power to the fan and the board, I use a 12V 3A power supply. The fan operates at 12V 0.2A, leaving plenty of headroom to power the board and anything else. However, the 5V supply is much more limited. And while trying to test the feasilibty of my next stage of this project, I found that using an RGB strip I have spare was simply too draining for the Arduino's buck converter, causing it to power off. Therefore, if I wish to proceed to the next stage, I will have to add an additional power source.

While I could buy a basic 5V power supply, or buy a 12V to 5V converter, I will instead use this as an opportunity to get some PCB designing skills. This will be discussed further in another blog post.

## Future Work:

I have already achived the main goals of stage one, with a temperature controlled fan that is resistant to sudden temperature spikes. However, I do have some work still to do that relates to stage 1, especially as stage 2 is delayed by power limits. 

Firstly, the Uno R4 Wifi has an LED matrix which I would like to use. I think I will implement 2 bars, one which shows the temperature on a scale of 0-100 and one for fan speed which will do the same. 

Secondly, I haven't implemented an actual fan ramp limiter which I still think would be a good idea to have, even if it isn't very relevant for my planned use case in a watercooling loop. 






