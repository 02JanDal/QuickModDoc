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

Name          | Type           | Required? | Description
------------- | -------------- |:---------:| ------------
formatVersion | int            | yes       | The version of the QuickMod format. Currently 1.
updateUrl     | string         | yes       | This URL should point at itself, and is used for updating it
uid           | string         | yes       | A java package style id of the QuickMod. Has to be globally unique to the QuickMod, and should __never__ change. `<author>.<modid>` is a good UID, but remember it may never change as long as it's still the same mod!
repo          | string         | yes       | A java package style repository id of the QuickMod. Has to be globally unique to your repository, and __never__ change. Two QuickMods with the same UID and repo are considered exactly equal and will overwrite each other.
versions      | version list   | yes       | A list of [versions](qm_versions_spec.html)
name          | string         | yes       | A descriptive, human readable name
modId         | string         | maybe\*   | The mod ID of the mod, as used by forge mods. It's the name (as used in the 'name' field in the .json file) if it's a LiteLoader mod.
description   | string         | no        | A description of the mod
license       | string         | no        | The mods license
urls          | object\*\*     | no        | An object of URL types
tags          | string list    | no        | A list of tags that apply to the mod
categories    | string list    | no        | A list of categories that apply to the mod. Tags and categories might often be more or less the same.
authors       | object\*\*\*   | no        | Authors that have participated in the creation of the mod
references    | object\*\*\*\* | no        | A list of all mods that are in some way referenced in the versions file

\* Required for forge and liteloader mods

\*\* A type -> URL list map. Types include 'website', 'wiki', 'forum', 'donation', 'issues', 'source', 'icon', and 'logo'. URLs are strings.

\*\*\* A role -> author list map. Roles and authors are strings.

\*\*\*\* A UID -> URL map. The URL value should be the same as the updateUrl of that mod. UIDs and URLs are strings.

## Reserved UIDs

In order to reduce the amount of fields, several UIDs are reserved and should be special cased by implementations. These include:

* `net.minecraftforge` - The supported version(s) of Forge
* `com.mumfrey.liteloader` - The supported version(s) of LiteLoader
* `net.minecraft` - The supported version(s) of Minecraft

These can be used for example as dependencies, but they do not need to be added to the root `references` object.

These also replace the old `mcCompat`, `forgeCompat` and `liteloaderCompat` fields.

## Example

Note: Most URLs etc in the below example won't work

```json
{
    "uid": "biomesoplenty.BiomesOPlenty",
    "modId": "BiomesOPlenty",
    "name": "Biomes O' Plenty",
    "repo": "github.glitchfiend",
    "description": "Biomes O' Plenty is a mod that is designed to give players a better Minecraft world to explore, and more of a reason to explore it in the first place. There are a lot of realistic biomes, some fantasy biomes, and other cool things we've added to the mod.",
    "urls": {
        "icon": [ "https://rawgit.com/Glitchfiend/BiomesOPlenty/master/icon.png" ],
        "logo": [ "https://raw.github.com/Glitchfiend/BiomesOPlenty/master/logo.png" ],
        "website": [ "http://www.minecraftforum.net/topic/1495041-" ],
        "source": [ "https://github.com/Glitchfiend/BiomesOPlenty" ]
    },
    "license": "CC-BY-NC-ND 4.0",
    "updateUrl": "https://rawgit.com/Glitchfiend/BiomesOPlenty/master/quickmod.json",
    "tags": [ "Biomes" ],
    "categories": [ "Wordgen", "Biomes" ],
    "authors": {
        "Founder": [ "Forstride" ],
        "Author": [ "Adubbz", "Amnet", "ted80" ],
        "Credits": [ "gamax92", "enchilado", "Tim Rurkowski", "Soaryn", "MineModder2000" ]
    },
    "references": {
        "codechicken.ForgeMultipart": "https://rawgit.com/Chicken-Bones/ForgeMultipart/master/FMP.json"
    },
    "versions": [
        {
            "references": [
                {
                    "uid": "codechicken.ForgeMultipart",
                    "version": "[1.0.0.228,)",
                    "type": "depends"
                },
                {
                    "uid": "net.minecraft",
                    "version": "1.6.4",
                    "type": "depends"
                }
            ],
            "sha1": "143be69351467fa7ddceaf23ee018b816ef2e702",
            "type": "Alpha",
            "name": "1.2.1.434",
            "version": "1.2.1.434",
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
