---
layout: post
title: Victoria - propulsion
---

After reading through many designs based on thrusters, surfboards, kayaks, trolling motors, and a variety of home built motors. I've settled on what I think is a fairly resilient, yet simple enough design.

### Drive

There will be one "main drive" powered by a [blue robotics motor](https://www.bluerobotics.com/store/thrusters/m200-motor-r1/) and a custom prop. There will also be two smaller "secondary drives" that are either [blue robotics t100 thrusters](https://www.bluerobotics.com/product-category/thrusters/t100-t200-thrusters/) or just motors, again with custom props. The secondary drive motors will be placed to either side of the boat to allow them to both control the direction, and act as a primary source of propulsion as needed.

The secondary drive mechanism will not be used at all unless at least one of the following occurs:

- The main drive faults
- The "rudder" faults

### Direction

Directional control will be provided by one of two means:

- A "rudder"
- Secondary drive motors

### "Rudder"

Instead of a traditional rudder I'm leaning towards simply rotating the main motor. If for some reason that proves to be ineffective, a traditional rudder will be used. I did some initial research into rudder sizing and shapes and efficiencies. It seemed overly annoying to properly plan a rudder location, size, and shape, that meshed well with the prop size and speed, and the hull shape and speed. Rotating the motor seems like a cheap way to avoid making a dumb mistake here.

Since I'm not sure of the proper name for the technique of rotating them otor, I'm still calling it a rudder. 

The rudder consists of:

- [A gear motor with encoder](https://www.pololu.com/product/2827)
- [A worm gear](https://www.servocity.com/html/vertical_shaft_worm_drive_gear.html#.VjBao66rSHo)
- [A motor controller](https://www.arduino.cc/en/Main/ArduinoMotorShieldR3)
- And a shaft with a bottom [bearing](http://www.amazon.com/Ceramic-Bearing-Yellow-Seal-8x22x7/dp/B00JQLGIUA) that semi-seals the shaft

The shaft and rudder electronics will all be contained in a watertight isolation from the rest of the boat internals to prevent leaks from damaging the rest of the boat internals.

The rudder electronics and motors will also all be located as far above the waterline of the boat as possible. Hopefully the combination of using the bottom bearing and worm gear bearing will keep water from exiting the shaft too much.

### Fault tolerance

Based on the design, it is required that at least *2* out of the 3 drive motors fault before the boat becomes inoperable. For Victoria's sake, hopefully that's enough.