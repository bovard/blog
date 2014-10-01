---
title: Archon
author: bovard
date: 2014-01-14 15:00
template: article.jade
---

In which I create my first npm package


<span class="more"><span>

#### Description

[Battle Code](http://battlecode.org/) is a yearly competition hosted by MIT.
Competitors design an AI to control robots to lead them to battle on the virtual battlefield!

After the first week of BattleCode most teams run into the same problem: over optimization.
By this I mean teams will watch themselves lose a match because they did `x` then
spend the next couple hours changing `x` to `y` only to learn that doing `x` actually
helped their bot win 9/10 times.

How can teams test against this? The immediate thing that comes to mind is to create
a few local test bots that have a variety of basic strategies implemented and test
your new changes against that set of bots on all the maps.

In [2013](articles/battle_code_2013/) we did this by hand and in 2014 I was determined
to provide a much more elegant solution to this problem.

Introducing: [archon](npmjs.org/package/archon)!

Want to run all your bots against all other bots on all the maps?

```
archon -m -t
```

Want to run your submission against all other submissions on all the maps?

```
archon -o teams/newSub -m -t
```

What's more all of those matches will be saved by default in the replays/ directory. You can queue
up to watch all the games locally with

```
archon watch replays/
```

#### Code

Archon was my first substantial hobby project in pure node.js and I don't think
I fully took advantage of things like Promises which would have made my life
a lot easier.

Basically archon writes to the Battle Code engine's config file called bc.conf:

```
# Match server settings
bc.server.throttle=yield
bc.server.throttle-count=50

# Game engine settings
bc.engine.debug-methods=false
bc.engine.silence-a=false
bc.engine.silence-b=false
bc.engine.gc=false
bc.engine.gc-rounds=50
bc.engine.upkeep=true
bc.engine.breakpoints=false
bc.engine.bytecodes-used=true

# Client settings
bc.client.opengl=false
bc.client.use-models=true
bc.client.renderprefs2d=
bc.client.renderprefs3d=
bc.client.sound-on=true
bc.client.check-updates=false
bc.client.viewer-delay=50

# Headless settings - for "ant file"
bc.game.maps=adobe
bc.game.team-a=teleportingplayer
bc.game.team-b=teleportingplayer
bc.server.save-file=match.rms

# Transcriber settings
bc.server.transcribe-input=matches\\match.rms
bc.server.transcribe-output=matches\\transcribed.txt
```

After we set `bc.game.team-a`, `bc.game.team-b`, `bc.game.maps` and a few other
settings we shell out `ant file` and listen to the results.

I think at this point I'm getting all I can out of my currently sloppy implementation,
if I were to have a bunch of features to add I'd probably redo a few things using
promises.

You can find the [code](https://github.com/bovard/archon) on my github. Feel free
to open an issue request or (better) a PR if you have something that you'd like to add.


#### Results

Archon has so far been a success. At the time of this writing it has 448 downloads
in the past month!


###### Written 09/26/2014


