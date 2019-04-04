---
layout: post
title:  Starting Pathfinder
date:   2019-03-29 22:03
categories: pathfinder
---
This started off as a Pathfinder project. There are more things that I want to do in the world than just write the code. I want to play and DM, but I'm fussy as hell about code. 

It's like doodling. I start by sketching out something rough and then I endlessly fiddle with the details. Based on the book, character generation flows something like this.

#### Step 1 - Starting Out
* Choose Name
* Choose Age
* Choose Sex
* Choose Race
* Choose Concept

I've actually got this done. No sweat. Literally just defining &-commands to store new attributes on the player.
	
#### Step 2 - Determine Ability Scores
* Roll Stats
* Choose Stat Array
* Assign Abilities
* Derive Ability Modifiers

This is where I've been spending most of my time, and I finally finished it today. I really should rewrite it with switch() because the code is tighter, but it is actually very readable right now.
	
#### Step 3 - Pick Your Race
* Choose Race
* Assign Racial Ability Bonuses
* Assign Racial Skill Bonuses
* Assign Racial Spell-like Abilities
* Assign Racial Feats

I actually moved the choose race to Step 1. this step really exists to take care of everything else related to race. I will probably skip this step for a while. It makes sense for a character to pick this stuff now, but I need to figure out how to represent skills and feats, and then figure out how to store the data.

#### Step 4 - Pick Your Class
* Choose Class
* Choose Favored Class (some races)
* Assign Class Abilities

Choosing the class is easy, but I need to figure out class abilities. For the most part, I think they will be handled like feats, but things like spells and a Monk's bonuses to saves and the like will have to be handled. This is probably the single hardest step.

#### Step 5 - Pick Skills and Select Feats
* Derive Starting Skill Points
* Assign Skill Ranks
* Assign Feats

This is almost certainly the thing I have to tackle next. Step 3 where I assign skill bonuses will happen concurrently with this. I can either use multiple delimiters to fake a Python style dictionary, or I can just have one attribute store one skill rank, another store miscellaneous modifiers, and then add the appropriate skill modifier. This would have been easier with D&D 5E.
	
#### Step 6 - Buy Equipment

I'd like to use actual objects and then register and somehow lock modifying the item. That way they can be moved around, described by the players, loaned, etc. It may wind up entirely softcoded, because unless it is a magic item, who really cares? Leather armor is leather armor.

#### Step 7 - Finishing Details
* Derive Hitpoints
* Derive Base Speed
* Derive Saving Throws
* Derive Armor Class
* Derive Initiative
* Derive Base Attack

Math. Just a bunch of math and making sure every part of the character sheet is filled in.