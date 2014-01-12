---
layout: index
title: The QuickMod file syntax
---

# The QuickMod file syntax

## File type

JSON file

## File ending

.json, .quickmod is also allowed, though .json is prefered

# The fields

Here's a listing of all fields currently defined

Name         | Type           | Required? | Description 
------------ | -------------- |:---------:| ------------
stub         | boolean        | no        | Only used internally. Set to true if the QuickMod file was generated from the mcmod.info file, and therefore only can be used as a placeholder.
uid          | string         | yes       | A java package style id of the QuickMod. Has to be globally unique for the QuickMod, and should NEVER change. <author>.<modid> is a good uid, but remember it may never change as long as it's still the same mod!
modId        | string         | maybe\*   | The mod ID of the mod, as used by forge mods.
name         | string         | yes       | A descriptive, human readable name
nemName      | string         | no        | The name of the mod in NotEnoughMods
description  | string         | no        | A description of the mod
iconUrl      | qmurl\*\*      | no        | A URL to an icon for the mod
logoUrl      | qmurl\*\*      | no        | A URL to a logo for the mod
websiteUrl   | qmurl\*\*      | no        | A URL to the mods website
issuesUrl    | qmurl\*\*      | no        | A URL to an issue tracker for the mod
donationsUrl | qmurl\*\*      | no        | A URL for leaving donations to the mod
updateUrl    | qmurl\*\*      | yes       | This URL should point at the QuickMod file, and is used for updating it
versionsUrl  | qmurl\*\*      | yes       | This URL should point at a [QuickMod Versions](qm_versions_spec.html) file
verifyUrl    | qmurl\*\*      | no        | This URL should point at a UTF-8 encoded file containing only a SHA512 checksum of this QuickMod file. If that checksum is correct the user will be given a nice message
tags         | stringlist     | no        | A list of tags that apply to the mod
categories   | stringlist     | no        | A list of categories that apply to the mod. Tags and categories might often be more or less the same.
authors      | object\*\*\*   | no        | Authors that have participated in the creation of the mod
references   | object\*\*\*\* | no        | A list of all mods that are in some way referenced in the versions file

\* Only if it's a forge mod

\*\* See _QuickMod URLs_

\*\*\* A string -> stringlist map, where the key is a role of the authors given in the stringlist

\*\*\*\* A string -> qmurl map, where the key is the uid of the referenced mod, and the value should be the same as the updateUrl of that mod

<a id="qmurl">
## QuickMod URLs
</a>
All URLs that are referencing something 'inside' the QuickMod system, like other QuickMod files, version files etc. can make use of a few additional schemes (a part from the standard http, https etc.).
These mostly exist for convenience and to reduce bandwidth usage.

### github://&lt;user&gt;@&lt;repo&gt;/&lt;filename&gt;[#&lt;branch&gt;]

Expands to https://raw.github.com/&lt;user&gt;/&lt;repo&gt;/&lt;branch&gt;/&lt;filename&gt; (default branch is master)

### mcf:&lt;topic-id&gt;

Expands to http://www.minecraftforum.net/topic/&lt;topic-id&gt;-

## Example

Note: Most URLs etc in the below example won't work

```json
{
    "uid": "biomesoplenty.BiomesOPlenty",
    "modId": "BiomesOPlenty",
    "name": "Biomes O' Plenty",
    "nemName": "BiomesOPlenty",
    "description": "Biomes O' Plenty is a mod that is designed to give players a better Minecraft world to explore, and more of a reason to explore it in the first place. There are a lot of realistic biomes, some fantasy biomes, and other cool things we've added to the mod.",
    "iconUrl": "github://Glitchfriend@BiomesOPlenty/icon.png",
    "logoUrl": "https://raw.github.com/Glitchfriend/BiomesOPlenty/master/logo.png",
    "websiteUrl": "mcf:1495041",
    "updateUrl": "github://Glitchfriend@BiomesOPlenty/quickmod.json",
    "versionsUrl": "github://Glitchfriend@BiomesOPlenty/quickmod.versions.json",
    "tags": [ "Biomes" ],
    "categories": [ "Wordgen", "Biomes" ],
    "authors": {
        "Founder": [ "Forstride" ],
        "Author": [ "Adubbz", "Amnet", "ted80" ],
        "Credits": [ "gamax92", "enchilado", "Tim Rurkowski", "Soaryn", "MineModder2000" ]
    },
    "references": {
        "codechicken.ForgeMultipart": "github://Chicken-Bones@ForgeMultipart/FMP.json"
    }
}
```

See the [QuickMod Versions](qm_versions_spec.html) spec for an example of a matching versions file.
