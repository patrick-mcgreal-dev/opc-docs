# Admin Game Builder

## Overview

Game building is currently time-consuming and error-prone, which makes it difficult to quickly produce new games. The Admin Game Builder aims to speed up game building, as well as make it accessible to non-technical users. As a bonus, it will also eliminate the need to involve developers when building and publishing games.

Users will be able to preview games whilst building them, save unfinished games, and publish finished games.

Think of the Custom Game Builder as a simple model. The process of customising a question is fast, error-free, and non-technical. The Admin Game Builder will do the same for games as a whole.

## The game building process

**Current:**

1. Dan creates game files in the codebase (markdown, images, slide configuration)
2. A developer pushes the game files to the staging app
3. Dan and Anna test the game in the staging app
4. A developer pushes the game files to the production app
5. Dan and Anna test the game in the production app
6. The game is made accessible to the public

**Proposed:**

1. Dan and/or Anna uses the Admin Game Builder to generate all game content (questions, images, slides, etc.)
2. Dan and/or Anna use the preview function to test the game
3. Dan and/or Anna saves and publishes the game without the need to involve developers

## How it works

### Game Properties

The **Game Properties** tab is the first thing we see on opening the tool.

This is where general game data, such as the title and image are entered. The options that determine how the game will be filtered in the Game Chooser can also be set here.

Setting the "Customizable" option allows us to set customizable questions in the **Questions** tab.

### Questions Tab

The **Questions** tab is where we add questions to the game.

On adding a question, a popup allows us to enter question data, such as the title, image, and answer. This will be very similar to the custom question dialog from the Custom Game Builder page. The popup will also include the option to generate a finishiing slide from the question. This can be edited on the **Finishing Slides** tab.

Questions can be reordered by grabbing the icon in the "reorder" column and dragging into a new position. They can be edited or deleted by opening the edit popup with the "edit" button.

### Finishing Slides Tab

The **Finishing Slides** tab is where we generate the final slideshow for the game.

In the previous section, we were able to choose whether to produce a finishing slide for each question. Any questions for which this option was chosen will have existing slides in the slide list. To add the corresponding answer slides, select "Add New", and complete the popup. The new answer slide can then be dragged into place below the corresponding question.

Towards the end of the finishing slideshow, we might want to slowly reveal the answer to a master puzzle over a few slides. These slides can be generated in the same way, and placed at the bottom of the list.

Slides can be reordered by grabbing the icon in the "reorder" column and dragging into a new position. They can be edited or deleted by opening the edit popup with the "edit" button.

### Preview Game Button

This button allows us to preview the game in a new window. 

We can be confident that the game will look and function identically to this when it is published.

### Save Game Button

This button allows us to save the game in its current state - whether finished or unfinished.

The game is not published at this point. It can be opened and edited anytime.

### Publish Game Button

This button allows us to publish the game and make it accessible to users.

After publishing, we can edit and re-publish the game without breaking any in-progress games.

## A quick technical note on hosting space

At the moment, we store all of our game data directly on Heroku - this is not ideal. Rather, we should reserve the hosting space on Heroku for adding new app features in the future.

As part of the Admin Game Builder project, we will move all text game data into the existing database. The images will be moved to the Amazon S3 storage account.

This future proofs the application - we no-longer have to worry about taking up valuable server space with game data.