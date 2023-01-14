# Important
Starting at version 2.9.0 of the [Inscryption API](https://inscryption.thunderstore.io/package/API_dev/API/), support for talking cards is already included in the API itself.

Starting at version 2.3.0 of [JSONCardLoader](https://inscryption.thunderstore.io/package/MADH95Mods/JSONCardLoader/), support for talking cards through JSON is already included, so there's no need to use this mod alongside it. All talking cards created with this mod are also backwards compatible with JSONCardLoader.

# Description
An Inscryption mod that lets you easily add talking cards with an animated portrait and dialogue all with a JSON file.

![Talking Card Example](https://i.imgur.com/oe779Ar.gif)

This mod is currently in its **beta** stage. There might be bugs. If you have trouble using this mod, please read the [FAQ](#FAQ)! And if the FAQ doesn't help you or your bug isn't mentioned in the FAQ at all, feel free to contact me on Discord: `kelly betty#7936`

**\[UPDATE 01.05.22]:** Emotion support has been added! Documentation is [here](#emotions).

# Installation
This mod’s only dependencies are BepInEx and the InscryptionAPI mod.

There are two ways of installing this mod: with the help of a mod manager (like r2modman or the Thunderstore Mod Manager) or manually.

#### Installation (Mod Manager)
1. Download and install [r2modman](https://thunderstore.io/package/ebkr/r2modman/) or the [Thunderstore Mod Manager](https://www.overwolf.com/app/Thunderstore-Thunderstore_Mod_Manager).
2. Install this mod and all of its dependencies with the help of the mod manager! 

#### Installation (Manual)
1. Download and install BepInEx.
    1. If you're downloading it from [its Github page](https://github.com/BepInEx/BepInEx/releases), follow [this installation guide](https://docs.bepinex.dev/articles/user_guide/installation/index.html#where-to-download-bepinex).
    2. If you're downloading ["BepInExPack Inscryption" from Thunderstore](https://inscryption.thunderstore.io/package/BepInEx/BepInExPack_Inscryption/), follow the manual installation guide on the Thunderstore page itself. This one comes with a preconfigured `BepInEx.cfg` file, so it's advised.
3. Download and install the [Inscryption API mod](https://inscryption.thunderstore.io/package/API_dev/API/) following its manual installation guide.
4. Find the `BepInEx > plugins` folder.
5. Place the contents of **"TalkingCardAPI.zip"** in a new folder within the plugins folder.


# The JSON File
Your JSON file for this mod **must have a name that ends in "\_talk.json"**. If your JSON file's name does not end in "\_talk.json", this mod will not find your file.

If you're using this mod, I **heavily encourage you** to use [this JSON Generator](https://tinyurl.com/TalkingCardAPI020) for making your JSON file. I wrote the schema for this generator myself, making sure to add as many descriptions and as much pattern-matching as I could to make the process easier for you.

Again, **I heavily encourage you** to use this JSON Generator: [link](https://tinyurl.com/TalkingCardAPI020).

Anyhow; the documentation.

Your JSON file should look like this:

```json
{
  "cardName": "",
  "faceSprite": "",
  "eyeSprites": {
    "open": "",
    "closed": ""
  },
  "mouthSprites": {
    "open": "",
    "closed": ""
  },
  "emissionSprite": "",
  "faceInfo": {
    "blinkRate": 1.5,
    "voiceId": "female1_voice",
    "voiceSoundPitch": 1,
    "customVoice": ""
  },
  "emotions": [
  ],
  "dialogueEvents": [
    {
      "eventName": "OnDrawn",
      "mainLines": [ "" ],
      "repeatLines": [
        [ "" ],
        [ "" ]
      ]
    }
  ]
}
```

I'm going to explain each field in detail below.

If you want to see an example of a \_talk.json file completed filled out, you can look at my [Talking Possum](https://github.com/KBMackenzie/InscryptionJSONDump/blob/main/TalkingPossum/JSON/Possum_talk.json) card. It has an animated portrait, dialogue codes and a custom voice.

### Overview

| Field          | Description                                                                  |
|----------------|------------------------------------------------------------------------------|
| cardName       | The name of an existing card.                                                |
| faceSprite     | The path to an image for your card's face.                                   |
| eyeSprites     | The path to the images for your card's eyes: open and closed, respectively.  |
| mouthSprites   | The path to the images for your card's mouth: open and closed, respectively. |
| emissionSprite | The path to an image for your card's eye emission.                           |
| faceInfo       | A bunch of details about your card, which will be explained below.           |
| emotions       | Your character's emotion sprites. Explained [here](#emotions).               |
| dialogueEvents | The dialogue for your card. Will be explained more in depth below.           |

### Sprite Images
The images used for the character's face should have the dimensions of a regular Inscryption Act 1 card portrait: That is, 114 x 94 pixels.

A good approach to making these face sprites is draw the face, eyes and mouth in different layers in your art program of choice and then exporting each layer separately!

### FaceInfo

| Field           | Description                                                                  |
|-----------------|------------------------------------------------------------------------------|
| blinkRate       | How often your character blinks. The higher, the more often they'll blink.   |
| voiceId         | Your character's "voice". Will explain more below.                           |
| voiceSoundPitch | Your character's voice's pitch. The higher the number, the higher the pitch. |
| customVoice     | A custom voice for your character. Will be explained below.                  |

"voiceId" can only be one of these three strings:
1. female1_voice
2. cat_voice
3. kobold_voice

Most talking cards in the game use the first and simply change the pitch.

#### Custom Voices
You can add a custom voice to your character instead of using one of the default voices. For that, all you need to is put the path to your audio file in the "customVoice" field.

The supported audio formats are MP3, WAV, OGG and AIFF!

Please use a very short audio file for your voice. Typically, you want only a very short 'vowel' sound for this, since it's going to be played in rapid repetition.

If you put anything in "customVoice", then the contents of the "voiceId" field will not matter.

### DialogueEvents

The "dialogueEvents" field is an array of dialogue event objects. If you're confused by this, you should use the generator I mentioned above: it makes this step much easier.

A dialogue event object has the following fields for you to fill:

| Field       | Description                                                                 |
|-------------|-----------------------------------------------------------------------------|
| eventName   | The "trigger" for this dialogue event.                                      |
| mainLines   | The main lines for your dialogue event: what is said when it first happens. |
| repeatLines | The lines to be repeated when this event plays a second, and so on.         |

The "eventName" field can have the following strings for triggers:

| Trigger                    | Description                                                    |
|----------------------------|----------------------------------------------------------------|
| OnDrawn                    | Plays when your card is drawn.                                 |
| OnPlayFromHand             | Plays when your card is played.                                |
| OnAttacked                 | Plays when your card is attacked.                              |
| OnBecomeSelectablePositive | Plays when your card becomes selectable for a positive effect. |
| OnBecomeSelectableNegative | Plays when your card becomes selectable for a negative effect. |
| OnSacrificed               | Plays when your card is sacrificed.                            |
| OnSelectedForDeckTrial     | Plays when your card is selected in the deck trial node.       |
| OnSelectedForCardMerge     | Plays before your card receives the sigil in the sigil node.   |
| OnSelectedForCardRemove    | Plays when your card is selected for removal.                  |
| OnDiscoveredInExploration  | ... I'm unsure about this one, actually.                       |
| ProspectorBoss             | Plays at the beginning of the Prospector fight.                |
| AnglerBoss                 | Plays at the beginning of the Angler fight.                    |
| TrapperTraderBoss          | Plays at the beginning of the Trapper/Trader fight.            |
| LeshyBoss                  | Plays at the beginning of Leshy's boss fight.                  |
| RoyalBoss                  | Plays at the beginning of Royal's boss fight.                  |
| DefaultOpponent            | I am... unsure if this one even works.                         |

# Dialogue Codes
A really neat feature of Inscryption's dialogue events are dialogue codes, which have many uses in dialogue.

The dialogue codes most relevant to talking cards will be explained below. All of these work with talking cards.

### Wait (\[w:])
This is by far the dialogue code you'll wanna use the most. It's also the one the game itself uses the most in all of its dialogue.

The "\[w:x]" dialogue code adds a pause of x seconds before the rest of a sentence plays.

You can use it like this:
```
"Hello.[w:1] How are you?"
```
In this example, after saying "Hello.", the character waits 1 second before saying "How are you?".

The number of seconds does not have to be an integer. Using "\[w:0.2]" to wait only 0.2 seconds is valid, for example, and used often throughout the base game's dialogue.

This being said, I'd advise you not to go below \[w:0.1], as I don't know how small the number can go before issues arise. (And there's no point in going below that, anyhow.)

### Color (\[c:])
The \[c:] dialogue code changes the color of a portion of your text.

You can use it like this:
```
"[c:R]This text is red.[c:] This text is not."
```
In this example, the part after \[c:R] is colored in the color that matches the code 'R', which is the color red, and the part after \[c:] has the default text color. You can think of this as "switching on" the colorful text mode and then switching it off.

*"But how do I know the codes for each color?"*
Fear not! Here's a comprehensive table of all available colors and their respective codes:

| Code | Color             |
|------|-------------------|
| B    | Blue              |
| bB   | Bright Blue       |
| bG   | Bright Gold       |
| blGr | Bright Lime Green |
| bR   | Bright Red        |
| brnO | Brown Orange      |
| dB   | Dark Blue         |
| dlGr | Dark Lime Green   |
| dSG  | Dark Seafoam      |
| bSG  | Glow Seafoam      |
| G    | Gold              |
| gray | Gray              |
| lGr  | Lime Green        |
| O    | Orange            |
| R    | Red               |

(For the record: These are the colors the game has available, built-in. I did not choose them. Yes, it's a very odd selection of colors.)

#### Custom Colors
I have added a way to use custom colors with dialogue codes. In place of one of the color codes in the table above, you can instead use a [hex color code](https://htmlcolorcodes.com/color-picker/), and this mod will parse the code into an usable Color for the text.

Here's an example:
```
"You must be... [w:0.4][c:#7f35e6]confused[c:][w:1].",
```
In this example, the word "confused" is colored in the color #7f35e6. Which, if you don't wanna look it up, is [this color!](https://g.co/kgs/JPHV5v)

### Leshy (\[leshy:x])
The \[leshy:x] dialogue code makes Leshy say x. This color code is very useful for making Leshy and your card talk a bit between each other!

You can use it like this:

```
"We're all doomed.[leshy:Quiet now.][w:2]",
```
In this example, the character says "We're all doomed." and then Leshy says "Quiet now." right after. The text remains on the screen for 2 seconds.

There are a few things to note from that example:

1. You don't need to put quotation marks around the line Leshy is going to say.
2. The "Wait" dialogue code is still usable with Leshy's lines.

# Emotions
All of the base game's talking cards have more than one emotion. Emotions are exactly what they sound like: Different facial expressions for a character to convey different emotions.

For those who care about this: Emotions are a C# `enum` in the game's code. This means each item has a numeric value associated with them.

Your character's default emotion is "Neutral". This emotion is added by default.

Anyway, a comprehensive list of all emotions, and the numeric value associated with each:

| Emotion  | Number |
|----------|--------|
| Neutral  | 0      |
| Laughter | 1      |
| Anger    | 2      |
| Quiet    | 3      |
| Surprise | 4      |
| Curious  | 5      |

There's another item in the Emotion enum, "None", but you should probably not use it.

To learn how to add emotions, see [this section](#adding-emotions).
To learn how to use emotions, see [this section](#using-emotions).

### Adding Emotions
You can include new Emotions for your card by adding them to the "emotions" array in your JSON file. This is what that should look like:

```json
"emotions": [
  {
    "emotion": "Anger",
    "faceSprite": "Example_AngryFace.png",
    "eyeSprites": {
      "open": "Example_AngryEyes_Open.png",
      "closed": "Example_AngryEyes_Closed.png"
    },
    "mouthSprites": {
      "open": "Example_AngryMouth_Open.png",
      "closed": "Example_AngryMouth_Closed.png"
    },
    "emissionSprite": "Example_AngryEmission.png"
  }
]
```

In the example above, a new emotion is added, "Anger", which changes the sprites for the character's face.

The "emotion" field should contain the name of a valid emotion. (See the table above!)

#### "Do I have to replace every sprite?"
You don't have to replace every single sprite when you make an emotion!

You can change only the fields you want to, and leave out the fields you don't want to change. The fields you leave out are ignored, and they "default" to the Neutral emotion's sprites for those fields.

See this example:

```json
"emotions": [
  {
    "emotion": "Anger",
    "eyeSprites": {
      "open": "Example_AngryEyes_Open.png",
      "closed": "Example_AngryEyes_Closed.png"
    },
    "emissionSprite": "Example_AngryEmission.png"
  }
]
```

In that example above, only the sprites for the eyes and eye emission are changed. The sprites for the face and mouth stay the same; that is, they default to the Neutral emotion's face and mouth sprites.

If you're still confused about how this works, I advise you use the JSON Generator I linked above. I wrote the schema for it myself, and it should help you with creating emotions (and everything else). You can even choose to toggle optional fields on and off, which is specially handy for emotions!

#### Side Note: Re-using Images
*"I want to re-use the same image multiple times! Will that affect performance?"*

This mod implements a little texture cache, so an image is always only loaded once regardless of how many times you use it in your JSON file. Because of this, you *don't* have to worry about using the same image multiple times.

This means if you *really want* to use the same image for a character's eyes across multiple emotions (and even across multiple characters), you can do so without fear of it affecting performance. 

#### Side Note: Empty Texture
You can add an 'empty'/fully transparent texture to a field if you wish, 'hiding' that field for a given emotion. This mod adds shorthand for that: "\_" (an underscore) in the image field.

Here's an example:
```json
{
  "emotion": "Quiet",
  "eyeSprites": {
    "open": "Example_EyesClosed.png",
    "closed": "Example_EyesClosed.png"
  },
  "emissionSprite": "_"
}
```

In that example, the emission is replaced by an empty texture, and is thus not displayed at all.

This has lot of uses: Hiding a character's eyes for one emotion, hiding emissions for one emotion, et cetera.

### Using Emotions
You can change your character's emotion in their dialogue lines, with the dialogue code `[e:x]`, where 'x' is the name of an emotion. You can look at the table above for the names of all the available emotions.

This mod adds patches to make the emotion names not case-sensitive, which means the following lines are all equally valid:

```
"[e:Anger]I'm angry."
"[e:anger]I'm angry."
"[e:AnGeR]I'm angry and my keyboard is acting up."
```

If you prefer, you can use the numeric value associated with an emotion instead of its name! This is perfectly valid, for example:

```
"[e:2]I'm angry."
```

# FAQ

**Q:** *"I'm getting an error that says my \_talk.json file couldn't be loaded! What does this mean?"*

**A:** Please double check your file and make sure you didn't make any mistakes with the JSON syntax.

There are multiple JSON validator tools you can use online that catch syntax errors and things of the sort. A favorite of mine is [JSONLint](https://jsonlint.com/).


# Changelog
- **0.2.1**: Added 'Important' note at the top, and made small changes in preparation to the new API/JSONCardLoader update.
- **0.2.0**: Major changes:
  - Added support for emotions!
  - Updated the JSON schema in the generator to now include emotions.
  - Fixed a bug with custom color codes that happened when those were used mid-sentence.
- **0.1.2**: - Fixed softlock on OnDrawn and some other dialogue events when no dialogue for that event was provided.
- **0.1.0**: - Initial upload.
# Special Thanks
Special thanks to Nevernamed (Bt Y#0895) on Discord for his help with setting up talking cards! c:

# Credits
This project uses [Newtonsoft.Json](https://github.com/JamesNK/Newtonsoft.Json) for parsing JSON data.

Newtonsoft.Json's license can be found [here](https://github.com/JamesNK/Newtonsoft.Json/blob/master/LICENSE.md).