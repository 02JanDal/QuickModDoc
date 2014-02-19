---
layout: index
title: The QuickMod Index file syntax
---

# The QuickMod Index file syntax

## File type

JSON file

## File naming

Always `index.json`

# Contents

A QuickMod Index file should contain a JSON object with the field `index` with an array as value. All QuickMod files contained in the repository should then be listed in the JSON array, one object each, with a 'uid' field and a 'url' field ([qmurl](qm_spec.html#qmurl) pointing at the QuickMod file).
If a field with the key `baseUrl` exists all relative URLs are resolved with that as base, or if it contains "{}" that is replaced by each items url.

# Usage

Mainly used for quickly getting larger amounts of QuickMod files to browse
