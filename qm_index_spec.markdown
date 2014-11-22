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

* baseUrl \(string, optional\): All 'url' fields in the 'index' array are resolved with this URL prefixed. If it contains "{}" (which is invalid in URL), those characters will be replaced with the contents of the 'url' fields in the 'index' array.
* index \(array\): See [below](#index).
* repo \(string\): If this is present, the index file will be remembered and refetched when the normal QuickMod files get updated. Has to be global unique but always the same for the same index.

### Index
An array of objects with the following properties:

* url \(string\): The url to a QuickMod File
* uid \(string\): A unique identifier for this mod, which should never change and be repeated in the linked to QuickMod file
