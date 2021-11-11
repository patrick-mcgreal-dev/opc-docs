# Pushing Custom Games to Production

There are two things that need to be done for the custom game changes to work in production.

## 1. Environment Variables

The AWS_BUCKET_NAME variable has been replaced with two new variables:  

- AWS_BUCKET_NAME_AVATARS="opc-production-avatars"
- AWS_BUCKET_NAME_GAME_IMAGES="opc-production-game-images"

## 2. Database Migration

There are three migration files that are part of the custom game changes:  

- 20210928122725-create-custom-question.js
- 20211019065711-create-custom-game.js
- 20211102101512-game-data-update-1.js

The third file is important. It updates the "gameData" column for all existing records in the "GameSessions" table.  

It's a good idea to make sure that active GameSessions still work after this migration. If the production app is in maintenance mode, we can do this check and avoid breaking any active GameSessions.