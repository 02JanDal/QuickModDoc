---
layout: index
title: The QuickMod file syntax
---

# The QuickMod file syntax

## File type

JSON file

## File ending

.qm, .quickmod or .json are allowed, .qm is prefered and should be used in most cases

# The fields

Here's a listing of all fields currently defined

Name         | Type           | Required? | Description 
------------ | -------------- |:---------:| ------------
formatVersion | int           | yes       | The version of the QuickMod format. Currently 1.
uid          | string         | yes       | A java package style id of the QuickMod. Has to be globally unique for the QuickMod, and should NEVER change. <author>.<modid> is a good uid, but remember it may never change as long as it's still the same mod!
repo         | string         | yes       | A java package style repository id of the QuickMod. Has to be globally unique for your repository, and NEVER change. Two QuickMods with the same uid and repo are considered exactly equal and will overwrite each other.
modId        | string         | maybe\*   | The mod ID of the mod, as used by forge mods.
name         | string         | yes       | A descriptive, human readable name
nemName      | string         | no        | The name of the mod in NotEnoughMods
description  | string         | no        | A description of the mod
license      | string         | no        | The mods license
urls         | object\*\*\*   | no        | An object of URL types
updateUrl    | qmurl\*\*      | yes       | This URL should point at the QuickMod file, and is used for updating it
tags         | stringlist     | no        | A list of tags that apply to the mod
categories   | stringlist     | no        | A list of categories that apply to the mod. Tags and categories might often be more or less the same.
authors      | object\*\*\*\* | no        | Authors that have participated in the creation of the mod
references   | object\*\*\*\*\* | no        | A list of all mods that are in some way referenced in the versions file
versions     | array          | yes       | A list of versions, see [here](qm_versions_spec.markdown) for documentation.
mavenRepos   | stringlist     | no        | A list of maven base urls to search for if a downloadType is maven, or for maven dependencies

\* Only if it's a forge mod

\*\* See _QuickMod URLs_

\*\*\* An object with keys being URL types and values being a list of qmurls. Possible types: website, wiki, forum, donation, issues, source, icon, logo.

\*\*\*\* A string -> stringlist map, where the key is a role of the authors given in the stringlist

\*\*\*\*\* A string -> qmurl map, where the key is the uid of the referenced mod, and the value should be the same as the updateUrl of that mod

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
    "urls": {
        "icon": [ "github://Glitchfiend@BiomesOPlenty/icon.png" ],
        "logo": [ "https://raw.github.com/Glitchfiend/BiomesOPlenty/master/logo.png" ],
        "website": [ "mcf:1495041" ],
        "source": [ "https://github.com/Glitchfiend/BiomesOPlenty" ]
    ],
    "license": "CC-BY-NC-ND 4.0",
    "updateUrl": "github://Glitchfiend@BiomesOPlenty/quickmod.json",
    "tags": [ "Biomes" ],
    "categories": [ "Wordgen", "Biomes" ],
    "authors": {
        "Founder": [ "Forstride" ],
        "Author": [ "Adubbz", "Amnet", "ted80" ],
        "Credits": [ "gamax92", "enchilado", "Tim Rurkowski", "Soaryn", "MineModder2000" ]
    },
    "references": {
        "codechicken.ForgeMultipart": "github://Chicken-Bones@ForgeMultipart/FMP.json"
    },
    "versions": [
        {
            "mcCompat": [ "1.6.4" ],
            "depends": {
                "codechicken.ForgeMultipart": "[1.0.0.228,)"
            },
            "name": "1.2.1.434",
            "installType": "forgeMod",
            "urls": [
                {
                    "url": "http://adf.ly/391097/http://files.minecraftforge.net/BiomesOPlenty/BiomesOPlenty-universal-1.6.4-1.2.1.434.jar",
                    "downloadType": "sequential"
                }
            ]
        }
    ]
}
```
