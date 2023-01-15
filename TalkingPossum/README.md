An Inscryption mod that adds an Opossum talking card. The talking Opossum card has custom dialogue and a custom voice.

The talking Opossum card has an animated portrait, custom voice, and multiple emotions!

![Talking Card Example](https://i.imgur.com/oe779Ar.gif)

In addition, this mod also adds 3 starter decks:
| Name           | Cards                               |
|----------------|-------------------------------------|
| Awesome Possum | Opossum (Talking), Opossum, Opossum |
| Death Tango    | Opossum (Talking), Cockroach, Cat   |
| Trash Mammals  | Opossum (Talking), Skunk, Raccoon   |

![Talking Opossum Decks](https://i.imgur.com/rlsiNAj.png)

The talking Opossum card also has a secret special ability added with Configils!

# A Small Note
**\[UPDATE 01.15.22]:** This mod was originally made as an example of how to use my [TalkingCardAPI](https://inscryption.thunderstore.io/package/KellyBetty/TalkingCardAPI/). Talking card support has finally already been merged into the core API (starting at version 2.9.0) and JSON support has been merged into JSONCardLoader (starting at version 2.3.0), so now TalkingCardAPI is no longer needed to use this Opossum card! Thanks everyone for the feedback! <3

# Installation
This mod’s dependencies are BepInEx, the InscryptionAPI, JSONCardLoader and TalkingCardAPI.

There are two ways of installing this mod: with the help of a mod manager (like r2modman or the Thunderstore Mod Manager) or manually.

#### Installation (Mod Manager)
1. Download and install [r2modman](https://thunderstore.io/package/ebkr/r2modman/) or the [Thunderstore Mod Manager](https://www.overwolf.com/app/Thunderstore-Thunderstore_Mod_Manager).
2. Install this mod and all of its dependencies with the help of the mod manager! 

#### Installation (Manual)
1. Download and install BepInEx.
    1. If you're downloading it from [its Github page](https://github.com/BepInEx/BepInEx/releases), follow [this installation guide](https://docs.bepinex.dev/articles/user_guide/installation/index.html#where-to-download-bepinex).
    2. If you're downloading ["BepInExPack Inscryption" from Thunderstore](https://inscryption.thunderstore.io/package/BepInEx/BepInExPack_Inscryption/), follow the manual installation guide on the Thunderstore page itself. This one comes with a preconfigured `BepInEx.cfg` file, so it's advised.
3. Download and install the [Inscryption API mod](https://inscryption.thunderstore.io/package/API_dev/API/) following its manual installation guide. You need version 2.9.1+ of the API to run this mod.
4. Download and install the [JSONCardLoader mod](https://inscryption.thunderstore.io/package/MADH95Mods/JSONCardLoader/) following its manual installation guide. You need version 2.3.0 of JSONCardLoader to run this mod.
6. Find the `BepInEx > plugins` folder.
7. Place the contents of **"TalkingPossum.zip"** in a new folder within the plugins folder.

# FAQ

**Q:** *"How can I make my own talking cards?"*

**A:** This mod was made entirely with JSON. You can use this mod as an example for reference / as an example if you want to make your own talking cards with [JSONCardLoader](https://inscryption.thunderstore.io/package/MADH95Mods/JSONCardLoader/)!.

If you want to see the `\_talk.jldr2` file for this Opossum card (and all of the other JLDR2 files, for that matter), I have put it all [here](https://github.com/KBMackenzie/InscryptionJSONDump/tree/main/TalkingPossum/JSON).

JSON is very accessible, you should try making your own JSON cards if you haven't already!

# Changelog
- **1.3.0** - TalkingPossum now uses JSONCardLoader v2.3.0 and no longer depends on TalkingCardAPI!
- **1.2.0** - Complete redesign + added emotions!
- **1.0.0** - Initial upload.