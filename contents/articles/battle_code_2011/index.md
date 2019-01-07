---
title: BattleCode 2011
author: bovard
date: 2011-02-05 15:00
template: article.pug
---

In which I abuse inheritance. Heavily.

<span class="more"><span>

#### Description

[Battle Code](http://battlecode.org/) is a yearly competition hosted by MIT.
Competitors design an AI to control robots to lead them to battle on the virtual battlefield!
Each robot is running on a separate thread so communication between bots is limited.


Fresh from my win in the Google AI Challenge, I recruited a team from there to head over
and do Battle Code. Unfortunately none of them wrote a line of code.
This dampened my spirits but I was ready to push forward!

|  |  |
| ----- | ----- | -----
| ![Flying](flying2.png)  | ![Light](light1.png) | ![Medium](medium2.png) | ![Turret](turret2.png) | ![Armory](armory2.png) |  ![Building](building2.png) |  ![Dummy](dummy2.png) | ![Factory](factory2.png) | ![Recycler](recycler2.png)

######A selection of buildings and units from 2012

This year's unique challenge was modular robots. To start with you chose a chassis
(heavy, medium, light, or flying). By default each chassis could sense obstacles 1 square in
each direction, receive messages, and carry a specified weight of components.
These components were broken into 4 categories: builders, sensors, weapons and communication.

You can read more about the details of the contest on the winning team's [post-mortem blog post](http://blog.stevearc.com/2011/12/17/battlecode-postmortem.html).
But lets just say the winning strategy involved heavy chassis with a teleport component, a hammer and a mountain of armor.

#### Code

Being a fresh graduate of a Java-based undergraduate program I did the first
thing that came to mind: misuse the #*%& out of inheritance.

What happened next was a Daily WTF-worthy inheritance tree:

```
RobotSystem
  ^-SensorRobotSystem
    ^-BuilderSensorRobotSystem
      ^-WeaponBuilderSensorRobotSystem
```

Not only does a WeaponBuilderSensorRobotSystem never build anything but also sometimes they don't have a sensor!
As the competition entered its final week I learned just how painful major refactors
are when the function you are calling could be in one of four files (or all four)! You can check out the code on my [github](https://github.com/bovard/robo-rumble).

Walking away from this I learned first-hand the perils of ignoring the `composition over inheritance` mantra.

#### Results

I placed about the middle of the pack overall but I was the 2nd place non-MIT team.

###### Written 03/22/2014


