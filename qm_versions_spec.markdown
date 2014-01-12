---
layout: index
title: The QuickMod Version file syntax
---

# The QuickMod Version file syntax

## File type

JSON file

## File ending

Add .versions infront of the file ending of the QuickMod file (<name>.json -> <name>.versions.json and <name>.quickmod -> <name>.versions.quickmod)

# The fields

The QuickMod Version file contains a JSON array of objects, here is a list of all the fields currently defined for the object:

Name | Type | Required? | Description
---- | ---- | --------- | -----------
mcCompatibility | stringlist | yes | A list of all Minecraft versions supported by this version
forgeCompatibility | interval\* | no | An interval of all forge versions supported
depends | object\*\* | no | A list of all mods this mod version has a strong dependency on
recommends | object\*\* | no | A list of all mods this mod version works well with, but that are not necessary for it to run
suggests | object\*\* | no | Like `recommends`, but even less strong
breaks | object\*\* | no | A list of all mods that this mod version breaks in some way, like crashes etc.
conflicts | object\*\* | no | A list of all mods that this mod version conflicts with, meaning it might not crash but there might be other unpleasent surprises.
provides | object\*\* | no | A list of all mods that this mod provides, meaning they shouldn't be installed side-by-side (Opis provides MapWriter, for example)
name | string | yes | A name for this version. Good if it matches the regular expression \d+(\.\d+)* (1.2, 4.5.2.3.2.4 etc.). See also [below](#note_versions)
downloadType | enum | no | The way this URL should be treated. If the value is `direct` the URL is followed directly and without showing anything to the user. `parallel` will start loading it in browsers together with all other `parallel` URLs. All `sequential` URLs will be loaded one-by-one, which is required by adfly etc. The default is `parallel`.
installType | enum | no | The way the received file should be treated. `forgeMod` is the default and means put into <minecraft>/mods/, `forgeCoreMod` means put into <minecraft>/coremods/, `configPack` means extract with <minecraft> as root. There is also `group` which means that nothing should be downloaded or installed for this version (except dependencies). Useful if there's an "umbrella" QuickMod file that will download all submods
url | url | yes | Not required if `installType` is `group`. This is the URL that will be followed for this version.

\* Interval notation, see [wikipedia](http://en.wikipedia.org/wiki/Interval_%28mathematics%29#Notations_for_intervals). Leave _a_ or _b_ empty for infinity

\*\* uid -> version interval mapping.

<a id="note_versions">
## A few notes on version naming
</a>

Psuedocode for how versions are compared:

```
function lessThan(string v1, string v2)
  stringlist parts1 = split v1 at '.'
  stringlist parts2 = split v2 at '.'

  while not parts1 and parts2 are empty
    string part1
    string part2
    if parts1 is empty
      part1 = "0"
    else
      part1 = pop from parts1
    if parts2 is empty
      part2 = "0"
    else
      part2 = pop from parts2

    if can convert part1 and part2 to int
      int num1 = part1 to int
      int num2 = part2 to int
      if num1 equals num2
        continue
      else
        return num1 lessthan num2
    else
      if part1 equals part2
        continue
      else
        return part1 lessthan num2

  return false
```

This means that subparts at which both versions can be converted to an integer are compared like integers (leading zeros discarded etc.), while if at least one of them cannot be converted to an integer they are compared according to the string comparison of the language in question.
This string comparison will of course differ between languages, but as long as a4b is greater than b3a, a3a and a4a you should be good to go.

## Example

```json
[
    {
        "mcCompatibility": [ "1.6.4" ],
        "depends": {
            "codechicken.ForgeMultipart": "[1.0.0.228,)"
        },
        "name": "1.2.1.434",
        "downloadType": "sequential",
        "installType": "forgeMod",
        "url": "http://adf.ly/391097/http://files.minecraftforge.net/BiomesOPlenty/BiomesOPlenty-universal-1.6.4-1.2.1.434.jar"
    }
]
```

See the [QuickMod](qm_spec.html) spec for an example of a matching QuickMod file.
