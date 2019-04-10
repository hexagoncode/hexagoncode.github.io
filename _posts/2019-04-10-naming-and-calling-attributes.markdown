---
layout: post
title:  Naming and Calling Attributes
date:   2019-04-10 09:08
categories: [ Dungeons and Dragons, Mushcode ]
---
I've made the switch to Dungeons & Dragons 5th Edition in earnest. I will return to Pathfinder at some point, but the mechanics of 5E are significantly easier to code for. However, I had not expected subraces.

Only some races have subraces. So far they are the format of <something> <race>, so Mountain Dwarf or High Elf. Every subrace adds more racial traits. I wonder if it might not be easier to treat them as separate but similar races code wise, but for the moment it seems to be arbitrarily easy to just treat it like a second race.

Racial traits fall into two categories: those that can be easily coded for and those that cannot. Increasing an ability score is easily coded. Gaining a bonus to your armor class, but only against specific kinds of enemies is not. What is the point when there are no coded monsters? Even if there were, that would be best checked in some sort of combat code. For items not easily coded, I am just listing them at the bottom of the character sheet.

Another example of easily coded are a character's age, size, languages, and (generally) speed.

At the moment, I am calling the easily coded ones "info", because the player needs to know it, and the difficult ones "traits". Traits will be appended to the sheet. Info will be evaluated and set during a final check step.

The code looks something like this:

```
&_5E.DWARF_INFO object=Dwarves are stout and hardy. Their age is X...
&_5E.DWARF_TRAITS object=Speed~Dwarves have a base wakling speed of 25 feet. Their speed is not reduced by wearing heavy armor|Darkvision...
&_5E.HILL_DWARF_INFO=Hill dwarves live in hills. They gain 1 hitpoint per level...
```
You can see how they are starting to get long, but I've kept them like this because they are easily indexed. Easily in terms of readability, not necessarily in terms of coding for access. It makes me wonder if I need to look at making a function, but I am not sure why just yet. 

When developing for multiple things, I need that first PF or 5E so I can see if the traits on the test player bit belong to this incarnation of the system or to something else. Just calling it _AGE could create some conflicts. I am tempted to go with a least specific data first approach and do "INFO_DWARF_HILL" but one of my goals is to make this code extensible by people who aren't the greatest coders. If you really want to add Orcs, you should be able to. And if there are Green Orcs and Gray Orcs, you should be able to figure that out easily, too. I am making heavy use of iteration and lists instead of hard coding that stuff into the character generation just to make that work.

I am considering using another delimiter, maybe the backtick (`) to help break it up.
```
&_GAME.CATEGORY`ENTRY_DATA
&_5E.INFO`HILL_DWARF
```

Just a thought. I already had to do something similar if I want to store a list of traits. See the above &_5E.DWARF_TRAITS and notice that I use a tilde (~) to divide item from description, and a pipe (\|) to divide each entry. Spaces and commas are straight out. I don't even know how many other delimiters I can get away with. Maybe @ and ^. MUX does understand multiple character delimiters like --, but I am not sure that every function does.

So how am I calling the data?
```
[u(#98/_5E.[first(get(%#/_5E.SUBRACE))]_[get(%#/_5E.RACE)]_INFO)]
```

So, we're evaluating the attribute name as we type it. Previously we set _5E.SUBRACE to "Mountain Dwarf", so we get the first word of whatever it is as the player bit can't have a subrace without a race. I don't want to deal with the underscore, so I just call race directly. I could just call the last() function, but I kind of like that this is a subtle check that the race is still set as well.