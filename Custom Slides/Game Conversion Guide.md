# Game Conversion Guide

## Overview

Previously, the finishing slideshow was composed of image files that would be shown in the order that they appeared in the `static/images/GAME_NAME/answers` folder. Introducing customizable questions means that these slides now need to be generated in a different way.

Under the new system, a "slide" is the combination of a markdown file containing the slide's text, and an image which will be displayed on the left-hand side. The markdown files containing the slide's text exist in three folders under the `games/GAME_NAME` directory: `questions`, `answers`, and `extras`.

The slide images exist in three identically named folders in the `static/images/GAME_NAME` directory. Each slide markdown file contains an `Image` tag in the header data, which tells the slideshow where to find the relevant image.

Finally, a `slides.json` file is required in the `games/GAME_NAME` directory. This file determines the order in which the slides are shown.

## 1. Create new folders

In the `games` directory, locate the folder of the game to be converted. Inside this folder, create the following additional folders:

1. `answers`
2. `extras`

In the `static/images` directory, locate the folder of the game to be converted. Inside this folder, create the following additional folders: 

1. `extras`

## 2. Add 'answer' slides content

**Relevant folder:** `games/GAME_NAME/answers`

In the finishing slideshow, we usually want to pair each question slide with an answer slide. This folder will contain markdown files that represent each of these answer slides.

As each question (with the possible exception of a master puzzle - we'll come to that later) requires an answer slide, the easiest way to begin is by copying the contents of the `GAME_NAME/questions` folder directly into this folder. After doing so, we have a collection of markdown files with the same names as the corresponding question files.

Inside each answer file, we require only the `Image` header tag. Clear out the rest of the header tags and replace "questions" with "answers" in the `Image` tag. The header data in each file should now look like this:

```
---
Image: GAME_NAME/answers/NAME_OF_IMAGE.png
---
```

The text in each answer file can be copied over from the old style answer slide, which can be found in the `static/images/GAME_NAME/answers` directory. Find the correct one, and copy the text over to the new answer file using markdown formatting. The complete answer file should now look something like this:

```
---
Image: GAME_NAME/answers/NAME_OF_IMAGE.png
---

# PUZZLE NAME

The explanation of the puzzle solution goes here.

**The puzzle question can be reiterated here, if necessary**

## The answer to the puzzle goes here
```

## 3. Add 'answer' slides images

**Relevant folder:** `static/images/GAME_NAME/answers`

This folder is where the old slides live, and it's being repurposed as the location of the images used by the answer files we just created. These images will be displayed alongside the answer explanation text.

For each answer file, locate the relevant answer slide and cut out the image portion into a new separate image. Save this image back to the folder, using the name from the `Image` header tag of the answer markdown file.

For example, if the answer file header data looks like this:

```
---
Image: GAME_NAME/answers/puzzle-1.png
---
```

...then your answer image file should be named `puzzle-1.png`.

## 4. Add 'extra' slides content

**Relevant folder:** `games/GAME_NAME/extras`

In the finishing slideshow, we might want to insert slides other than question/answer pairs at various points. One use case might be a multi-slide buildup to the reveal of a master puzzle. This folder is where these extra slides will live.

For each extra slide required, create a markdown file in this folder. It's useful to start each filename with a number that represents the order in which they'll be used, just to keep things neat. Here's an example from the extras folder belonging to "A Very Meta Chrismas":

```
00-masterp-0.md
01-metaverse.md
02-kfc.md
03-mari-lwyd.md
04-goat.md
05-le-befana.md
06-masterp-1.md
07-masterp-2.md
08-masterp-3.md
```

The header data for each markdown file in this folder requires an `Image` tag and an `Extra` tag. The `Image` tag should point to an image in the `static/images/GAME_NAME/extras` folder (we'll generate this image in the next step), and the `Extra` tag should always be set to `true`. 

The content area of the file can contain anything, so long as it's valid markdown.

Overall, the file should look something like this:

```
---
Image: GAME_NAME/extras/NAME_OF_IMAGE.png
Extra: true
---

# This is a header

This is some content.

**This is some bold text**
```

## 5. Add 'extra' slides images

**Relevant folder:** `static/images/GAME_NAME/extras`

This is the folder in which we'll add the images that our extra slides are pointing to. For each extra slide, make sure an image exists in this folder with the name referenced in the `Image` header tag.

## 6. Set the display order of slides

**Relevant folder:** `games/GAME_NAME`

All of the content for our slides has now been created, and we're just missing the file that tells the app the order in which to show them. In the `games/GAME_NAME` directory, create a file called `slides.json`.

The contents of this file needs to be surrounded by square brackets, so copy and paste the following into the new file:

```
[
    
]
```

To add a slide to the finishing slideshow, we insert an object between these square brackets with the following format:

```
{
    "type": "markdown",
    "folder": "",
    "file": ""
}
```

The `"type"` tag will always be `"markdown"`, except in one special case which we'll come to later. 

The `"folder"` tag refers to one of the three folders that now exist in the `games/GAME_NAME` directory: `questions`, `answers`, and `extras`.

The `"file"` tag refers to the name of a markdown file that exists in the chosen folder.

Here's an example of a `slides.json` file with a pair of question/answer slides - note the commas between each one:

```
[
    {
        "type": "markdown",
        "folder": "questions",
        "file": "puzzle-1"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "puzzle-1"
    },
]
```

At some point in the finishing slideshow, we might want to show a slide containing all of the answers. This can be inserted into the `slides.json` file with the following object:

```
{
    "type": "all-answers"
},
```

This special object doesn't require the `"folder"` or `"file"` tags.

As an example, here's the complete `slides.json` file for "A Very Meta Christmas":

```
[
    {
        "type": "markdown",
        "folder": "extras",
        "file": "00-masterp-0"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "01-coins"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "01-coins"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "02-codes"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "02-codes"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "03-solve"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "03-solve"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "04-wanda"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "04-wanda"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "05-mag"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "05-mag"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "06-elves"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "06-elves"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "07-shib"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "07-shib"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "08-sets"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "08-sets"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "09-squid"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "09-squid"
    },
    {
        "type": "markdown",
        "folder": "questions",
        "file": "10-movies"
    },
    {
        "type": "markdown",
        "folder": "answers",
        "file": "10-movies"
    },
    {
        "type": "all-answers"
    },
    {
        "type": "markdown",
        "folder": "extras",
        "file": "01-metaverse"
    },
    {
        "type": "markdown",
        "folder": "extras",
        "file": "02-kfc"
    },
    {
        "type": "markdown",
        "folder": "extras",
        "file": "03-mari-lwyd"
    },
    {
        "type": "markdown",
        "folder": "extras",
        "file": "04-goat"
    },
    {
        "type": "markdown",
        "folder": "extras",
        "file": "05-la-befana"
    },
    {
        "type": "markdown",
        "folder": "extras",
        "file": "06-masterp-1"
    },
    {
        "type": "markdown",
        "folder": "extras",
        "file": "07-masterp-2"
    },
    {
        "type": "markdown",
        "folder": "extras",
        "file": "08-masterp-3"
    }
]
```

## 7. Testing

Now that the game has been converted to the new format, it's a good idea to create a game session to test that the slides are all formatted correctly and being shown in the correct order.