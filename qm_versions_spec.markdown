---
layout: index
title: The QuickMod Version object syntax
---

# The QuickMod Version object syntax

The QuickMod Version objects can contain the following fields:

Name | Type | Required? | Description
---- | ---- | --------- | -----------
mcCompat | string list | yes | A list of all Minecraft versions supported by this version
urls | object\*\* list | yes | A list of possible URLs (mirrors)
name | string | yes | A name for this version. See [below](#note_versions)
version | string | no | This can be used if you use a versioning scheme not compatible with semantic versioning. Set `name` to "your" version and `version` to a semantic version compatible value
forgeCompat | [interval](#interval) | no | An interval of all forge versions supported
liteloaderCompat | [interval](#interval) | no | An interval of all liteloader versions supported
references | object\* list | no | A list of all dependencies, conflicts etc. etc.
type | string | no | A type of the version, for example Release, Dev, Alpha or Beta.
installType | enum | no | See [below](#installtype)
sha1 | string | no | The checksum of the downloaded file
libraries | object\*\*\* list | no | A list of libraries required by the mod version

\* Object which has the field 'uid' and optionally '[type](#reftype)', 'version' and 'isSoft'. 'version' is a version interval. If it doesn't exist, the latest compatible version will be used. If 'isSoft' is true (default is false) and the 'type' is 'depends' this mod will not be removed when the referenced mod is removed. Make sure to add this to 'references' in the top level of the QuickMod.

\*\* Object with the field 'url' and optionally '[downloadType](#downloadtype)' and 'priority', which helps the client select a mirror

\*\*\* Object with the fields 'name' and optionally 'repo'. The 'name' should be in the format `<group>:<artifact>:<version>`. 'repo' defaults to [Maven Central](http://central.maven.org/maven2/). If provided, it should be an absolute URL to a maven repository. 

<a id="downloadtype">
## Download Type
</a>

Possible values of the`downloadType`field:

Value | Description
----- | -----------
direct | Don't display a browser, just download the URL directly
parallel | Loaded at the same time as all other`parallel` URLs
sequential | Loaded one-by-one, needed by adfly or similar URLs
encoded | See [Encoded URLS](#encoded)

`parallel`is the default.

<a id="encoded">
## Encoded URLs
</a>
It may be possible in the future to encode urls, so that only someone in the possesion of a password can use it. To do so, create a URL object with the 'downloadType' set to 'encoded'. Next, encode the URL (algorithm TBD). Add a hint that tells the user where/how to get the key for decrypting and optionally add a "group" that will be used to detect if two keys are the same (same group = same key) so the user won't have to enter the key every time.

NOTE: This is not implemented in MultiMC and it's only a draft. Do not use, as it will likely break or it may become deprecated due to possible legal issues.

<a id="installtype">
## Install Type
</a>

Possible values of the`installType`field:

Value | Description
----- | -----------
forgeMod | Load using classpath
forgeCoreMod | Put into`<minecraft>/coremods/`
liteloaderMod | Save with .litemod extension and load by giving to LiteLoader using a CLI argument
extract | Extract at`<minecraft>`
group | Don't download or install anything, except dependencies.

`forgeMod`is the default.

`group`is useful for "umbrella" mods. Example: ProjectRed does not contain any files, it just depends on the ProjectRed-\* mods.

<a id="reftype">
## Reference Type 
</a>

Value | Description
----- | -----------
depends | The mod must be installed
recommends | The mod should be installed
suggests | It would be nice of the mod was installed
conflicts | The mod cannot be installed
provides | The mod can be replaced by the referencing mod

It may be hard to see the difference between depends, recommends and suggests, partly because it's may be very subjective.
Example: MFR recommends Buildcraft for power generation, while Railcraft only suggests it, as Railcraft has it's own power generation, and AdditionalBuildcraftObjects depends on it

<a id="interval">
## Interval Notation
</a>
[Interval notation](http://en.wikipedia.org/wiki/Interval_%28mathematics%29#Notations_for_intervals) is a way of describing a set of numbers, or in this case, versions. Leave _a_ or _b_ empty for infinity. Using reverse brackets instead of parenthesis is not supported. Examples:

    [1.0.0,)      # 1.0.0 ≤ v
    (1.0.0,)      # 1.0.0 < v
    (,2.0.0)      #         v < 2.0.0
    (,1.9.9]      #         v ≤ 1.9.9
    (0.1.0,2.0.0) # 0.1.0 < v < 2.0.0
    [1.0.0,2.0.0) # 1.0.0 ≤ v < 2.0.0


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

# Example

See the [QuickMod](qm_spec.html) spec for an example.
