  ---
  layout: post
  title: Embedded Systems Module - Final Assessment
  ---

This blog post will look back at my final assessment for my embedded systems module during bachelor's degree.

## The Assessment:

The overall assessment was based around simulating very basic robots. A server in the university was set up, and when sent a properly formatted request it would provide the initial starting information for a simulation. This would include the number of robots, their position in the world, and their heading. We would then have the simulate the robots according the parameters laid out in the brief and display the output on a screen. 

4 Types of robots where laid out:
1. Simple robots which travelled in a straight line unless they interacted with another robot.
2. Chasers, which would attempt to follow other robots if they came within a certain distance.
3. Evaders, which would attempt to move away from other robots.
4. Stalkers, which would attempt to follow other robots but would move away if they got too close.

The whole simulation was to be created on a Zybo Z7-10 FPGA board which has an FPGA and 2 ARM cores. The aim of the asssessment is to create the fastest possible simulation while retaining accuracy. This was to be achieved by using smart software tricks to avoid costly calculations, and use hardware acceleration from the FPGA where possible. 

The assessment was programmed in C, with softcores created in C++, using the Vitis IDE (A reskin of Eclipse). Hardware designs were designed and generated in Vivado.

## Networking:

The first part of the assessment required sending and recieving packets from the university server, in the correct format, such that they could be decoded. This required using Vivado to attach the inbuilt ethernet port to the Zynq processor. We then created a program to send data in the required format to the correct IP. This was not too difficult as usually only one packet had to be sent. The harder part was creating a program to recieve the setup of the simulation as there were multiple packets, the data in the packets could vary in length, and they were padded with unnecessary data. In some of the harder scenarios, we would have to send multiple requests to the server before all the simulation data was recieved. 

This part of the assessment wasn't too problematic. I had a few issues converting the bitsteam into the correct data format due to some of the padding misaligning the bits. But that was quickly resolved, leaving me with no other issues with networking for the assessment.

## HDMI:

I am discussing out of order here, but the last part of the assessment required taking the live data from the simulation and outputting it to a screen via HDMI. As part of the assessment, we were provided with a vivado design that would allow us to use the HDMI output on the board, as well as some code to help us use it. This made implementing HDMI outputs relatively easy, but we still had to correctly format the data from the simulation such that is could be displayed to the screen, and send the correct commands to the output buffer so the frames could be displayed.

## Simulation:

The simulation was the most resource intensive and complicated part of the project when performance optimisation is included. We had to model the movement of all the robots in the world, and calculate the effects of collisions when required. The world was a 1440x900 grid and all robot movements would be calculated at the same time in discrete time steps. I broke this problem up into two parts, first the robots would calculate the desired moves they wanted to make, and then I calculated the effects of those moves and the results of any collisons that would have occured. This proved to be effective, and I managed to make an acceptable simulation.

## Optimisation and FPGA:

As the goal of the assessment was performance, I took several steps to improve the speed of calculations. Simple steps I took were ignoring the square roots when using pythagoras' theorm to calculate distances, instead comparing use squared values, as square rooting is a costly calculation that was not necessary for accuracy. I also precalculated Sine and Cosine values which I would need, storing every results between 0 and 360, in 1 degree increments, for both trigmetric function. This traded memory space for computation time, which was fine as memory space was not an issue. And lastly, I used integers instead of floating point values to record positions of the robots. This traded simulation accuracy about the robots position in exchange for computation time. However, to reduce the loss of accuracy I used multiple integer values to represent single points on the world grid. Specifically, I used 8 as this is a power of 2, meaning at the end it could be easily converted back into the correct value without a costly divison or the use of floating point operations. 

All these steps were enough to have the simulation running at the required FPS, however I wanted to improve the performance further and I had a whole FPGA to use. Calculating where the robots wanted to move and calculating their actual moves both required a set of for loops which iterated over the array of robots. This is an operation that could easily be parallelised. I chose to focus on the first step, where robots decide which direction they want to move in. I had some trouble with this at first as debugging a softcore due to the added complexity using an FPGA. I was not getting the correct output, and it appeared no data was being changed. But eventually I was able to figure out where the miscommuncation was happening, and ultimately I was able to significantly improve performance of the simulation by parallelising a large portion of the calculations through the FPGA. 

## Final Throughts:

It is approaching 4 years since I took this module, and looking back has been a positive experience. I was mildly optimistic when I first took the module, and by the end I had a new found passion for embedded software engineering. I found the optimisation, the different style of programming, and the access to physical devices to be far more appealing than standard software engineering. I was also good at it, which helped a lot. This module also first introduced me to C and C++, and lead onto my final year bachelor's project. I hope to one day come back to FPGAs, either in the workplace or as hobby project when the time is right. But my newest project involves an Arduino, which is a new adventure that I am looking forward to. 
























