---
layout: index
title: QuickMods
---

## What's this QuickMod thing?

A QuickMod file is a JSON file that contains metadata about a mod for the sandbox game Minecraft. This metadata can be things like name, description, authors, different URLs (website, issue tracker, donations etc.), but also machine readable information about how to install the mod.

## What's it for?

These QuickMod files can be given to a Minecraft launcher, for example MultiMC 5, and that launcher will then resolve any dependencies the mod has, download it and put in the right place. Using the different metadata the launcher can also allow you to search or browse for mods.

The QuickMod spec also allows for download links to require user interaction, which allows them to be adf.ly links. Remember that it's a lot more convenient for users if they don't have to do anything though.

## How does it work?

![Flowchart](images/QuickModFlowchart.png)
