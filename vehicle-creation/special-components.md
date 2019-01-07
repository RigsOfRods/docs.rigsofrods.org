---
layout: page
categories: [vehicle-creation]
title: "Special components"
---

# Command hydraulics - `commands`

[Documentation](/vehicle-creation/fileformat-truck/#commands)

A&nbsp;command is a beam&nbsp; that has "Commands"&nbsp;that make it extend/retract and so forth, 
The command beam has many uses, From being a Hydraulic arm to a destruction tool,
Some of the things you can do with commands... 

* Open hoods 
* Make lifting arms 
* Adjust ride heights
* Make extending parts
* Make winches 
* Many, many more uses too!

One example (in picture below) - all of the moving parts are made by using Commands:

![commands-wrecker](/images/commands-example-t800-wrecker.jpg)

# Connection utilities

This is a guide how you can use the different connection methods in RoR.

* `ties`: these are beams that grab a node and pull them tight
* `ropes`: like ties, just don't tighten itself
* `hooks`: nodes that interlock with other nodes or ropables

## Ropables

The documentation about ropables [can be found here](/vehicle-creation/fileformat-truck/#ropables)

## Ties

The documentation about ties [can be found here](/vehicle-creation/fileformat-truck/#ties)

Ties (as commands) can only work over an RPM of 800 and might request more power from the engine when being used.

So basically define a tie on the transport truck and a ropable on the load you want to tighten.

## Hooks

The documentation about hooks [can be found here](/vehicle-creation/fileformat-truck/#hooks)

Hooks lock against nodes in a search area of 40 centimeters.








