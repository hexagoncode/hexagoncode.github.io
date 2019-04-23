---
layout: post
title:  Leveling Up and Archiving Characters
date:   2019-04-23 08:36
categories: Dungeons and Dragons
---
With 5E, level drain is gone. Creatuers that once bestowed negative levels now just drain life or strength. Fantastic. That makes my job easier. But what if you want to automate advancement? 

I have been reluctant to add in any mechanic that is my own, but the character sheet will likely be a design I create based only loosely on the paper sheet. That gives me a little freedom, since I know there is no way it will be "pristine" and only reflect the design philosophies of the game developers.

## Leveling Up
Character advancement in 5E is incredibly formulaic, which is part of the reason I switched to it from Pathfinder. There are no skill ranks. There are no feats, though they are available as an advanced feature. Even multiclass spell lists, which were once astonishingly redundant are now merely daunting.

Here is a breakdown of leveling up:

#### Select Class
As 5E allows for multiclassing, characters can elect to advance in another class. There are prerequisites, but these can be checked when the player selects to advance in a class. If the character is adding a new class, there will be additional work (setting up spell slots, picking spells, choosing domain, etc.)

#### Increment Level
Increment class level and character level.

#### Increment Proficiency Bonus
Proficiency bonus is based on total character level, so this is just an easy lookup.

#### Add New Class Features
If the class is a new class, I will have to see if some of their required features exist. If not, they will have to add them. This is probably the wooliest part of the advancement because it will sort of duplicate character creation. Spells will be handled with the increment spell slots stuff. I should have the basic code, but I have to come up with a way to present it. Perhaps the whole thing needs some sort of "interface", because I would really like to provide the player with an advancement summary. 

#### Ability Score Improvement
Check for an ability score improvement. This happens at 4/8/12/16/19 and abilities cannot exceed 20.

#### Calculate Hit Points
Roll a dX appropriate to the new class. A history of rolled hit die should be kept on the character for each level. The new dX is added to that, and the whole history is summed. Then add constitution modifier multipied by character level. If your constitution increases, it retroactively applies to the character's hit points.

#### Check Racial Features
Some races, such as dragonborn, have features that level as they do. My initial inclination is to just leave it as text and the player can roll the increased breath weapon as they advance. I am considering having the text be sensitive to the character level so it doesn't give more information than it needs to and keeps things concise. On the other hand, a player might like to have that for advancement.

Additionally, some races have racial spells. Those will need to be added to an actual spell table. Basically their race will get a spell section, like a caster class.

#### Check Class Features
This is potentially the hardest part, and I have to review every class feature to see. I am not sure if any will actually change proficiencies or derived stats. I expect most to be text, though some things like the barbarian's rage will require a level based lookup.

#### Increment Spell Slots and Select Spells
Spell slots are determined by the following formula: One half ranger/paladin levels, rounded down, plus cleric/druid/sorcerer/warlock/wizard levels. Then just look it up on the advancement chart. Players will need to be able to pick new spells based on the class they pick. 

How to pick spells, though? I don't feel like reproducing the text of each, so I think just a leveled lookup list.

## Archiving Characters
The nice thing about prepending every relevant attribute with 5E is that I can iterate through the character and create a snapshot of their advancement. Some data, such as rolled hit point values, has to be retained to calculate the final value on the character sheet. But if a mistake is made, if some sort of spell or effect is used to regress a character, or even if cheating is suspected, it would be nice to have a snapshot of the character at advancement.

My thought is that the advance command creates an object with the current set of 5E values before any actual advancement takes place. This object should probably be created in a staff only area. Since advancing would likely work on the live data, once advancement starts it should not be exited from, just like character creation.