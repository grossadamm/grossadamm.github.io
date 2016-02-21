---
layout: post
title: Victoria - Rudder Turning
---

### The Good ###

The rudder moves! It's pretty neat rotating the compass and watching the rudder rotate with it. :)

### The Bad ###

I am using the [Arduino Motor Shield R3](https://www.arduino.cc/en/Main/ArduinoMotorShieldR3) for my motor control and I am having trouble not using it as a shield. I chose it since it provided easy current and voltage monitoring to track if my rudder motor was seized. 

I was hoping I could run jumpers between it and the arduino but that is not working out since the shield never powers up. Perhaps my temporary power source is not up to the task? 

The next surprising challenge has been sourcing nylon mounting for the arduino. I have not found any local stores that stock the m3 size required, so I have to order online. A silly problem, but one that has made progress halt while the order ships.

### The No Longer Bad ###

But the biggest hurdle was tracking down a memory leak. Since I'm new to C++ and embedded at that, I was treating arrays and pointers incorrectly causing a multitude of memory leaks. I had no idea until my Arduino started rebooting every 5 minutes. But the last of the leaks (I hope) is gone! Either way, the long term project definitely needs to handle Arduino reboots more frequently than I expected.

I'm also getting much better at soldering. At first I was not using flux since I didn't even know about it. Adding flux made a world of difference. I'm also starting to notice that my cheap soldering iron gets too hot to make decent runs. I'm hoping to use a printed board once I have the final circuit design done, but I'll still need to solder the components onto the board.