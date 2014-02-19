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

The QuickMod Version file contains a JSON object of objects, here is a list of all the fields currently defined for the object:

Name | Type | Required? | Description
---- | ---- | --------- | -----------
mcCompat | stringlist | yes | A list of all Minecraft versions supported by this version
forgeCompat | interval\* | no | An interval of all forge versions supported
references | objectlist\*\* | no | A list of all dependencies, conflicts etc. etc.
name | string | yes | A name for this version. See [below](#note_versions)
downloadType | enum | no | See [below](#downloadtype)
installType | enum | no | See [below](#installtype)
md5 | string | no | The checksum of the downloaded file
url | url | yes | This is the URL that will be followed for this version. Not required if`installType`is`group`

\* Interval notation, see [wikipedia](http://en.wikipedia.org/wiki/Interval_%28mathematics%29#Notations_for_intervals). Leave _a_ or _b_ empty for infinity

\*\* an array of objects, where each object has the field 'uid', 'type' and 'version'. Type can be any of 'depends', 'recommends', 'suggests', 'conflicts', 'provides', and version can be either empty or a version interval.

<a id="downloadtype">
## Download Type
</a>

Possible values of the`downloadType`field:

Value | Description
----- | -----------
direct | Don't display a browser, just download the URL directly
parallel | Loaded at the same time as all other`parallel` URLs
sequential | Loaded one-by-one, needed by adfly or similar URLs

`parallel`is the default.

<a id="installtype">
## Install Type
</a>

Possible values of the`installType`field:

Value | Description
----- | -----------
forgeMod | Put into`<minecraft>/mods/`
forgeCoreMod | Put into`<minecraft>/coremods/`
extract | Extract at`<minecraft>`
configPack | Extract at`<minecraft>/configs`
group | Don't download or install anything, except dependencies.

`forgeMod`is the default.

`group`is useful for "umbrella" mods. Example: ProjectRed does not contain any files, it just depends on the ProjectRed-* mods.

<a id="note_recommends">
## Depends vs. Recommends vs. Suggests
</a>

It may be hard to see the difference between depends, recommends and suggests, partly because it's may be very subjective.
Example: MFR recommends Buildcraft for powergeneration, while Railcraft only suggests it, as Railcraft has it's own powergeneration, and AdditionalBuildcraftObjects depends on it

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

This means that subparts at which both versions can be converted to an integer are compared like integers (leading zeros discarded etc.), while if at least one of them cannot be converted to an integer they are compared according to the string comparison of the language in question, meaning 1.10a might be less than 1.9a.

## Example

```json
[
    {
        "mcCompat": [ "1.6.4" ],
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
