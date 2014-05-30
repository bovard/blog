---
title: BattleCode 2013
author: bovard
date: 2013-02-01 15:00
template: article.jade
---

In which we win great victories.

<span class="more"><span>

#### Description
[Battle Code](http://battlecode.org/) is a yearly competition hosted by MIT.
Competitors design an AI to control robots to lead them to battle on the virtual battlefield!
Each robot is running on a separate thread so communication between bots is limited.

After not getting around to writing an entry for 2012 I was a bit ambivalent about
participating in 2013 but after it was clear that I had a good team that was actually
going to contribute, I was in!

This year's challenge involved a rock, paper, scissors-like strategies: nuke, rush and econ.
Each player started out with a base that could spend time doing one of two things: spawning
soldiers (took 8 turns) or doing research (anywhere from 100 - 400 turns). Every soldier was the same and they could find special
'encampment' squares and transform themselves into one of the encampment types
(artillery, generators, power supply, med base or shield). The game ended when your soldiers
destroyed the enemy hq or you were able to research nuke (took about 400 rounds).

The rush strategy was basically that, rushing your soldiers over to the enemy hq! The two bases were separated
by at least 50 rounds (or so) of navigation. Which meant that you could spawn a soldier
and by the timeit got to the enemy base it would be 2v1. That's assuming that the
enemy didn't spawn any encampments (which is usually a good bet that they did). The rush
was incredibly powerful in the first week due in part to its lower barrier of entry
and limited scope.

The nuke strategy was also pretty straight-forward: build a nuke. There was a lot of subtle
variations on this: how many soldiers should I build? should I only build if there
is an artillery spot near my base? only if I'm in a corner? etc...

Finally there was the econ strategy. For every generator and power supply you built you were able
to build soldiers faster and support more soldiers (respectively). In the econ strat
you invested to varying degrees in econ in hope of overwhelming the enemy late-game.

#### Code

For our main logic structure for the bots we used something called a decision tree.
Basically we created a tree structure in which every node had a pre/post condition and
an action. Additionally there were selector nodes, which would select a child action
to run based on the environment. The loop ran something like this:

```
observe_environment()
choose_action_from_tree()
execute_action()
```

This allowed up to build up several different trees to rapidly build out different
soldier roles that could be easily composed and switched. Here's a list of the more interesting
roles:

  * Backdoor soldier (run around the edges of the map to attack from behind)
  * Encampment hunter (checks enemy encampment spots while avoiding combat)
  * Miner (laid mines around the base)
  * Defender (defended the hq)

You can find the [code](https://github.com/bovard/BC2013) on my github.

#### Results

We ended up going to the finals at MIT! but lost out (0-2) while there giving us
somewhere in 9th-16th place.

###### Written 05/05/2014
