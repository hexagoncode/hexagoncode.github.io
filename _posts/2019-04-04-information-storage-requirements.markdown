---
layout: post
title:  Information Storage Requirements
date:   2019-04-04 14:31
categories: pathfinder systems
---
I am going to need to make some decisions. What do I want to model and what do I want to leave up to the players? Are my existing attributes names scalable? 

I can ignore things like _PF.STATLOCK because I will void all of that with whatever character approve command I come up with. Everything on the character sheet will need to be stored on the player object, whether it is the value, calculation, or reference to another attribute.

Do I want to call _PF.STRENGTH every time?

I'm making it a personal requirement that it is all prefaced with PF. I have the 5E project, and this could potentially just be d20 with little adjustment at that point. 

STRENGTH is fine, but I think STR may be better. Even the books use STR, DEX, CON, INT, WIS, and CHA. I do reference several things by referring to the attribute name when callling a list, so that would be a change. So I think I will continue to call each explicitly. I don't know the maximum length for an attribute name, but I know they can be extensive because the @name of exits are very long.

Currently, the code looks something like this:

```
&_PF.FULLNAME me=Feral Darkblade
&_PF.CONCEPT me=A test subject.
&_PF.CLASS me=Barbarian
&_PF.RACE me=Half-Elf
&_PF.AGE me=30
&_PF.MIDDLEAGED me=0
&_PF.ROLLED me=11 8 16 4 10 13
&_PF.ROLLED? me=1
&_PF.STATS me=11 8 16 4 10 13
&_PF.ARRAYCHOICE me=Rolled
&_PF.ATTRBONUS me=Charisma
&_PF.STRENGTH me=11
&_PF.STRENGTHMOD me=+0
&_PF.DEXTERITY me=8
&_PF.DEXTERITYMOD me=-1
&_PF.CONSTITUTION me=16
&_PF.CONSTITUTIONMOD me=+3
&_PF.INTELLIGENCE me=4
&_PF.INTELLIGENCEMOD me=-3
&_PF.WISDOM me=10
&_PF.WISDOMMOD me=+0
&_PF.CHARISMA me=13
&_PF.CHARISMAMOD me=+1
&_PF.STATLOCK me=1
```

I was very pleased when I found out that +2 and 2 are semantically identical in MUX. Also, note the attributes that begin with an underscore. Those attributes are only visible to objects that are set Wizard. So a player using @decompile on themselves will not see these things. 

It is all very legible so far, and I like legible. This may eventually bite me with something like _PF.SKILL_HANDLE_ANIMAL_RANKS. I need to seriously consider going to camelCase or using underscore delimiters to break apart long attribute names.

Going back to what I want to model I expect to arrive at the following:
* Dice that can roll a stat by name against a difficulty. Ex: roll Handle Animal=15 to roll Handle Animal against a DC of 15
* The full character sheet, including spells and familiars
* Basic inventory, whether by object or by attribute
* Equippable items that modify the character sheet code
* Light levels

What I expect to come later, or never at all:
* Fully programatic combat
* Grid-based combat
* Feats and special abilities that modify the character sheet code
* Enchanting system