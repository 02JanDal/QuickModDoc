---
layout: index
title: The QuickMod Index file syntax
---

# The QuickMod Index file syntax


## File Type
JSON File

## Distinction
If the 'index' property exists, the QuickMod file is an index.

## Contents
An object with the following properties:

* baseUrl \(string, optional\): All 'url' fields in the 'index' array are resolved with this URL prefixed.
* interpolate \(boolean, default: false\): If true, baseUrl must be present. Instead of prefixing baseUrl, any occurence of the characters '{}' will be replaced with the contents of the 'url' fields in the 'index' array.
* index \(array\): See [below](#index).

### Index
An array of objects with the following properties:

* url \(string\): The url to a QuickMod File
* uid \(string\): A unique identifier for this mod, which should never change and be repeated in the linked to QuickMod file
