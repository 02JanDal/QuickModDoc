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

| Name | Type | Required? | Description |
|------|------|:---------:|-------------|
| stub | boolean | no | Only used internally. Set to true if the QuickMod file was generated from the mcmod.info file, and therefore only can be used as a placeholder. |
| uid  | string | yes | A java package style id of the QuickMod. Has to be globally unique for the QuickMod, and should NEVER change. |
| modId | string | maybe\* | The mod ID of the mod, as used by forge mods. |
| name | string | yes | A descriptive, human readable name |
| nemName | string | no | The name of the mod in NotEnoughMods |
| description | string | no | A description of the mod |
| iconUrl | url | no | A URL to an icon for the mod |
| logoUrl | url | no | A URL to a logo for the mod |
| websiteUrl | url | no | A URL to the mods website |
| issuesUrl | url | no | A URL to an issue tracker for the mod |
| donationsUrl | url | no | A URL for leaving donations to the mod |
| updateUrl | qmurl\*\* | yes | This URL should point at the QuickMod file, and is used for updating it |
| versionsUrl | qmurl\*\* | yes | This URL should point at a [QuickMod Versions](qm_version_spec.html) file |
| tags | stringlist | no | A list of tags that apply to the mod |
| categories | stringlist | no | A list of categories that apply to the mod |
| authors | object\*\*\* | no | Authors that have participated in the creation of the mod |
| references | object\*\*\*\* | no | A list of all mods that are in some way referenced in the versions file |

\* Only if it's a forge mod
\*\* See QuickMod URLs
\*\*\* A string -> stringlist map, where the key is a role of the authors given in the stringlist
\*\*\*\* A string -> qmurl map, where the key is the uid of the referenced mod, and the value should be the same as the updateUrl of that mod

## QuickMod URLs

All URLs that are referencing something 'inside' the QuickMod system, like other QuickMod files, version files etc. can make use of a few additional schemes (a part from the standard http, https etc.):

### github://<user>@<repo>/<filename>[#<branch>]

Extends to https://raw.github.com/<user>/<repo>/<branch>/<filename>
