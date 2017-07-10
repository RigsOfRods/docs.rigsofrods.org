---
layout: page
title:  "Weight tuning"
categories: [tools-tutorials]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Introduction

<b><font color="red">SUMOWEIGHT ?</font></b> 

**A guide to tune your trucks to a realistic weight**

I will try to explain here how to tune your trucks weight without loosing it characteristics.
A lot of things have changed with the recent physics updates and there is no need for overweighted trucks at all in ROR anymore.


This guide is based on RoR version 0.36.3+.


All templates in this guide are free to use, you dont need to give any credits.

Why go for a realistic weight ? Well, RoR gets more and more realistic pyhsics in the last updates, so i think for gameplay and especially multiplayer trucks should have realistic weights in the future, so loading, lifting and crashing stuff works propper.
Since the new physics support this, here is your tutorial:

Here we go...first of all a template truck:

![Lightweight-truck](/images/lightweight-truck.png)

<b><font color="red">300 kg... RoR's first working 200 km/h light weight truck</font></b> 

[Download here](/download/lightweight.truck)

Its a truck featuring independent suspended front wheels and a rigid rear axle, it has a realistic steering geometry and is basically built for baja(gravel) terrains.

Overall weight including wheels is 300 kg, featuring working wheel nodearms and a small aerodynamic help for drifting and jumping ( to avoid zips its visible in the template file )

Spawns in the street cars (146) category.


<b><font color="green">Step by step weight tuning</font></b>

# Minimass

[Truck file format - minimass](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#minimass)

```
minimass
5.0
```

Even lower settings are fine. You need to add loadweight to every single node for weight tuning. Please refer to the template truck.

You can use [set_node_defaults](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#set_node_defaults) for group loadweights here too, but tweaking single nodes does not work and so its not recommended

A minimass setting lower then you minimum loadweight to a node makes no sense and will not provide any benefit.

# Set_beam_defaults

[Truck file format - set_beam_defaults](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#set_beam_defaults)

```
set_beam_defaults 12000000, 350, 200000, 2000000
```

A  good setting for rigid truck parts like suspension and frame with low weight nodes.

For lightweight nodes always use LOW damping settings, if you want parts of your truck deform propper while crashing, play around with spring, deform and brake values.

NEVEREVER use high dampings, they are responsible for truck explosions at spawn most of the times.

# Wheels

[Truck file format - wheels](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#wheels)

```
wheels
0.45, 0.3, 10,  13,  11,9999, 1, 1,  20, 22.5, 5000.0, 600.0, tracks/wheelface tracks/wheelband1
```

Really light weight wheels wich work fine with light trucks. 

If the wheels collapse too often or explode when hitting a wall, gently add some kg and test until you are fine. 

Increasing the spring rate gently works fine too. Test in small steps until you are satisfied.

# Overall weight

[Truck file format - globals](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#globals)

```
globals
50.0, 500.0, tracks/beam
```

A significant low starting weight helps to make trucks light.

Please note: Your load weight in this line ( second entry ) should be at least the total loadmass of you nodes, better higher. 

it does NOT apply to the truck weight if you set it higher then the actual sum of your loadweights.

# Shocks

[Truck file format - shocks/shocks2](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#shocks)

```
shocks2
;front axle
  10,   3, 8500, 1250, 5, 5, 8500, 1250, 5, 5, 1, 1, 1.05, vs
```

Use LOW shock settings now, especially the damping really needs to be LOW (less than 5k) for testing


If your trucks spawns stable, gently alter spring and damping settings until you are fine with the suspension works.

Overall guideline: lightweight trucks use low numbers ;)

# Engine/Engoption/Brakes

[Truck file format - engine](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#engine)

```
engine
1350.0, 3350.0, 350.0, 4.1, 1.8, 1.8, 1.8, 1.1, 0.8, 0.7, -1.0

engoption
0.125, c, 55, 0.4, 0.8, 0.4

torquecurve
gas

brakes
600
```

Low settings for torque, brakes and clutch avoid exploding wheels at higher speeds and while braking hard.

# Fusedrag

[Truck file format - fusedrag](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#fusedrag)

```
fusedrag
   3,   0, 0.25, NACA0009.afl
```

Your truck not accelerating propper and wheels spinning fast ? Use a small fusedrag.

# Testing

Open RoRConfig -> Debug tab -> Select "Beam Break Debug". This will log broken beams to the RoR.log file (Located in `Rigs of Rods/logs/RoR.log`), a vital tool for weight tuning.

So now spawn your truck, enter it and see it explode.


If it does not explode, you didnt push the limits hard enough, if you are fine with you weight and it works for you, you are successfully understood and managed to use the contents of this tutorial.


Else, you need to see if the truck desintegrates or the wheels explode. You might enable the replay mode in the confuigurator and use it to see.


If the trucks "walks/strafes" around your wheels are too light or their damping is too high. Fix that and try again

If the truck explodes or simply some beams break, exit ror and open your ror log (Located in `Rigs of Rods/logs/RoR.log`)

Search for "xxx" in the log file, the first entry is the beam that broke first. Write down the node numbers, open you truck file and add some kg to both of the nodes.

Spawn your truck and do this until you can spawn your truck without braking one single beam

When you managed to spawn your truck without any broken beam, start testing it. You might find some more beams that brake when jumping/landing hard or using commands etc.

Procedure is always the same, look into you RoR.log file, identify the nodes wich were attached to breaking beams and gently rise their weight until you got them working propper.

Overall, this way of weight tuning should lead to a fast and simple way to build really light weight trucks.









