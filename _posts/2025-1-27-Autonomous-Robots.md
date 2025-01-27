---
layout: post
title: Autonomous Robots Module - Final Assessment
---

This blog will look at my final assessment for my autonomous robots module from my masters degree:

## The Assessment:

The aim of the assessment was to create and test simulated robots in an artificial environment. We could use up to 3 robots, and they had to collect items and bring them back to a home area. The main goal of the assessment was to create several systems for picking up obstacles and then compare them. There was no set criteria for what was considered a better robot system, we had to build the systems and determine appropriate tests and metrics for comparing them. 

Most parts of the assessment were simplified to focus on the main goals of the assessment. Picking up items simply required driving a robot up to it. Dropping an item off only required driving to a dedicated home zone, which was quite a large area. The world was simple with no moving obstacles except the other robots, and only a few station obstacles. 

## Tools:

We had several tools available to us to help us create solutions for this assessment.

The robots were equipped with LIDAR sensors which could detect obstacles 360 degrees around itself, including other robots. But the LIDAR could not detect the items which had to be collected. It also had a long refresh cycle, making it unreliable when trying to detect other robots.

IMU sensors were also available to the robots, allowing them to detect their own acceleration, both deliberate and accidental. This had several potential uses such as detecting crashes and accounting for drift in the motors. 

Front facing cameras allowed the robots to see the environment infront of themselves. Along with this, we were provided with 3 computer vision algorithms. The first could identify the home zone from the camera. The second could identify items and their type. The third could identify other robots. All three algorithms would provide information on the size of the target in the frame and the location of the target in the frame. We were then able to use this information in whatever way we saw fit. 

Position tracking which uses the robots other sensors to know where the robot is in the world, including an estimation for how accurate the position data is.

NAV2 Navigation stack which allows the robot to set target coordinates and preplan a safe route to reach them with the help of prior world knowledge.

Finally, we could freely communicate between the robots with whatever information we wanted, assuming we could put it into an appropriate format. This included making a central server which communicated between the three robots and made decisions on its own. 

## My Aims:

I set out with several design goals and priorities for this assessment. 

Firstly, I wanted my code to be modular, as ROS2 is quite a modular system so I wished to embody that with what I produced. This required breaking a lot of functionality into submodules which could then operate for any robot with the required components. 

Secondly, I wanted to prioritse safety over productivity. This meant the robots should first make decisions based around avoiding collisions, before moving to collect items.

Finally, my tests for the assessment would compare different systems for assigning targets for the robots. So I had to design multiple reasonable systems for assigning targets. 

## Design:

Following my design goals, my first priority was safety. With the tools provided I created several systems of various levels of priority for deciding how the robots identify and deal with threats. 

The safety measures I implemented are using the camera to identify other robots within a robots path and taking actions to avoid them. Having the robots share their position with each other so they can identify robots that are straying too close even if they can't see them. And using LIDAR to detect solid obstacles. 

The robots would react to these various threats, generally by moving away from them and towards a safer location, in order of what seemed to be the greatest danger. However, I did also account for when avoiding a collision isn't possible, due to errors or otherwise. If the robots tried to move immediately after a crash, it could cause issues with their understanding of their position in the world due to conflicting data between the IMU and LIDAR. To resolve this, in a crash, the robots would immediately stop sending any movement commands to the wheels and wait for any effects of the crash to subside. Then they would attempt to move away from the danger before continuing their journey.

But more important than avoiding and accounting for crashes, was avoiding situations where a crash could occur. This is where the NAV2 navigation stack comes in, as it allows the robots to plan routes that avoid potential conflicts in the first place. There are other steps to reducing the opportunites for collisions too, which I will discuss shortly.

With most of the safety aspects established, I moved onto productivity. This required making the robots move out into the world to collect items and then bringing them back to the home zone. The locations of the items is not known by the robots, nor are they visible on LIDAR, so the only way to find them is through the camera. Fortunately, the world was small so the robots would almost always be able to see some items. From there, the robots only had to be able to drive in a straight line towards whatever item they wanted to collect. Or, if they couldn't see an item, they would drive to a predetermined position and look for an item. And if that failed, they would randomly but safely navigate around, looking for an item. 

Once an appropriate item was collected, the robot would navigate back to pre determined location in the homezone, or use the camera to find the homezone if the usual navigation stack was unavailable. 

Where I decided to focus my experiments was on how robots would decide which items to collect. Items had different values, and the items more distant from the home zone tended to be of greater value. So I created several systems for assigning how the robots would pick which items to collect.

One system gave each robot a different type of item to collect, with the exact order being based on the robots initial starting location and what seemed to be the most optimal assignment.

The second assignment system allowed multiple robots to collect the same type of item, and the robots would choose based on what seemed best at the start of the test. 

The third assignment system made every robot collect the type of item, regardless of what appeared to be most optimal. 

I also had a random assignment system, but that was purely as a control. 

Why I chose to change the assignment systems was for 3 reasons. One was safety. By allowing the robots to pick more optimal and different item types, they would be less likely to move close to each other which would reduce the risk of collisions and the need for evasive maneuvers. The second was productiviy. Avoiding collsions wastes time which reduces productivity, and allowing the robots to focus on the most optimal items increases productivity by reducing travel time. Thirdly, there was also value in collecting the items which were more distant, as they may be more productive to collect than items that appeared immediately closer. 

As such, I tested the multiple systems to see which were the safest (had the fewest collisions), and were the most productive. 













