---
layout: index
title: The QuickMod Index file syntax
---

# The QuickMod Index file syntax

Index files can be used by bigger repositories to give hints about all links in that repository

## File type

JSON file

## File naming

Always `index.json`

# Contents

A QuickMod Index file should contain a JSON object with the field `isIndex` set to true. All QuickMod files contained in the repository should then be listed in the JSON object, with the UID as key and a [qmurl](qm_spec.html#qmurl) pointing at the QuickMod file.
If a field with the key `baseUrl` exists all relative URLs are resolved with that as base.

# Usage

Mainly used for quickly getting larger amounts of QuickMod files to browse
