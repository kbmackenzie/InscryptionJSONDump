Here you'll find instructions on how to make your own talking card with JSONCardLoader.

JSONCardLoader supports the following features for talking cards:
- Custom animated portrait
- Custom talking card dialogue, responding to many game events
- Custom voice sound for your talking card, added through a short audio file
- Support for facial expressions that you can change in your dialogue

All of this is done through JSON. You don't need to load any Unity prefabs or anything of the sort for your portrait either: All you need are some image files, which you'll referencing in your JSON file.

# Preparation
You're going to need an existing card for this. You can create your own card with JSONLoader! The instructions for it should be in JSONCardLoader's Thunderstore page.

You're also going to need to make another JLDR2 file for this. This new file will contain all of the necessary information for the generation of your talking card.

This new JSON file **must have a name that ends in "\_talk.jldr2"**. If your file's name does not end in "\_talk.json", you will run into quite a few issues, so please make sure of that!

I'm gonna explain the structure of "\_talk.jldr2" files below.

# Structure
Alright, for starters you're using this mod, I **heavily encourage you** to use [this JSON Generator](https://tinyurl.com/TalkingCardJSON) for making your JSON file. I wrote the JSON schema for this generator myself, making sure to add as many descriptions and as much pattern-matching as I could to make the process easier for you.

Again, **I heavily encourage you** to use this JSON Generator: [link](https://tinyurl.com/TalkingCardJSON).

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
  "emissionSprites": {
    "open": "",
    "closed": ""
  },
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

#### Note: Backwards Compatibility
I have included backwards compatibility for all cards created with my TalkingCardAPI mod before it was merged with JSONLoader. Most fields are the same, except for "emissionSprites", which didn't exist back then: Instead, JSON files back then had a "emissionSprite" field, which accepted only one image (for an 'open eye' emission only). Thus, you can still use that field, though I'd encourage you to transition to the new structure instead!

### Overview
An overview of every field in your JSON file, each of which will be explained in depth below:

| Field           | Description                                                                   |
|-----------------|-------------------------------------------------------------------------------|
| cardName        | The name of an existing card.                                                 |
| faceSprite      | An image for your card's face.                                                |
| eyeSprites      | A pair of images for your card's eyes: open and closed, respectively.         |
| mouthSprites    | A pair of images for your card's mouth: open and closed, respectively.        |
| emissionSprites | A pair of images for your card's eye emission: open and closed, respectively. |
| faceInfo        | A bunch of details about your card, which will be explained below.            |
| emotions        | Your character's emotion sprites. Explained [here](#emotions).                |
| dialogueEvents  | The dialogue for your card. Will be explained more in depth below.            |


### Sprite Images
All of the images used for the character's face (including eyes, mouth and emission) should have the dimensions of a regular Inscryption Act 1 card portrait: That is, 114 x 94 pixels.

A good approach to making these face sprites is draw the face, eyes and mouth in different layers in your art program of choice and then exporting each layer separately!

You don't have to worry about any performance impact when putting the same image on multiple fields, as [explained in this section below](#side-note-reusing-images).

This mod also includes shorthand for an 'empty' texture, which you can use when you want a part of your character's face to not be displayed. The shorthand for that is a "\_" in the field for the given image. This is [explained more in depth in this section below](#side-note-empty-textures).

### FaceInfo
A set of details about your character's face: blink speed and voice.

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

| Field       | Description                                                                     |
|-------------|---------------------------------------------------------------------------------|
| eventName   | The "trigger" for this dialogue event.                                          |
| mainLines   | A set of lines that plays in the very first time this event runs.               |
| repeatLines | Multiple sets of lines that are played after the first time this event has run. |

Each of these fields will be explained way more in depth below!

#### EventName
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
| ProspectorBoss             | Plays at the beginning of the Prospector fight.                |
| AnglerBoss                 | Plays at the beginning of the Angler fight.                    |
| TrapperTraderBoss          | Plays at the beginning of the Trapper/Trader fight.            |
| LeshyBoss                  | Plays at the beginning of Leshy's boss fight.                  |
| RoyalBoss                  | Plays at the beginning of Royal's boss fight.                  |

#### Main Lines
A set of lines that will be played in **very first time** that trigger runs for your card. The game remembers this. After the first time it plays, these lines will not play again for that same save file.

If you want these lines to ever play again, you can put them inside of the "repeatLines" array, which I'll explain below.

#### Repeat Lines
All the sets of lines that will be played in alternation each time this trigger runs for your card.

This field is a little funny, because it's an array of arrays! If you don't know what means, don't worry. This means you can have multiple sets of lines inside of repeatLines, like this:

```json
"repeatLines": [
  [
     "This is a perfectly valid set of lines.",
     "It ends here."
  ],
  [
     "This is another perfectly valid set of lines.",
     "This one ends here."
  ]
]
```

If you're still confused about how these work, I heavily encourage you to use the JSON Generator I linked above. The schema I wrote for it includes full support for adding repeat lines.

# Dialogue Codes
A really neat feature of Inscryption's dialogue events are dialogue codes, they add a lot of life to dialogue!

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

Please note that for compatibility reasons, your hex color code **should include the '#'**.

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
    "emissionSprites": {
      "open": "Example_AngryEmission_Open.png",
      "closed": "Example_AngryEmission_Closed.png"
    }
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
    "emissionSprites": {
      "open": "Example_AngryEmission_Open.png",
      "closed": "Example_AngryEmission_Closed.png"
    }
  }
]
```

In that example above, only the sprites for the eyes and eye emission are changed. The sprites for the face and mouth stay the same; that is, they default to the Neutral emotion's face and mouth sprites.

If you're still confused about how this works, I advise you use the JSON Generator I linked above. I wrote the schema for it myself, and it should help you with creating emotions (and everything else). You can even choose to toggle optional fields on and off, which is specially handy for emotions!

#### Side Note: Reusing Images
*"I want to re-use the same image multiple times! Will that affect performance?"*

This mod implements a little texture cache, so an image is always only loaded once regardless of how many times you use it in your JSON file. Because of this, you *don't* have to worry about using the same image multiple times.

This means if you *really want* to use the same image for a character's eyes across multiple emotions (and even across multiple characters), you can do so without fear of it affecting performance. 

#### Side Note: Empty Texture
You can add an 'empty'/fully transparent texture to a field if you wish, 'hiding' that field. This mod adds shorthand for that: "\_" (an underscore) in the image field.

Here's an example:
```json
{
  "emotion": "Quiet",
  "eyeSprites": {
    "open": "Example_QuietEyes_Open.png",
    "closed": "Example_QuietEyes_Closed.png"
  },
  "emissionSprites": {
    "open": "Example_QuietEmission_Open.png",
    "closed": "_"
  }
}
```

In that example, the 'closed eyes' emission is replaced by an empty texture. This means the emission vanishes when the character blinks!

This is very useful for eye-centric emissions.

This has lot of other uses: Hiding the emission altogether, hiding a character's eyes or mouth for a given emotion, et cetera.

### Using Emotions
You can change your character's emotion in their dialogue lines with the dialogue code `[e:x]`, where 'x' is the name of an emotion. You can look at the table above for the names of all the available emotions.

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