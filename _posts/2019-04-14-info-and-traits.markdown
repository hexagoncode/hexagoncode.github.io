---
layout: post
title:  Info and Traits
date:   2019-04-14 21:49
categories: Dungeons and Dragons
---
Spent most of the weekend creating dictionaries of information for the races, as they are somewhat simpler to do than the classes. I thought it would be a good chance to evaluate calling data.

So far I have created "info" and "traits". Info contains a blurb about the race and any abilities that will be coded onto the character sheet via another function. These tend to be things that will be called (such as ability scores) or are highly unique to the character (such as age). Traits are those things that can only be easily represented by pure text and will require the player to make adjustments on the fly. A good example of this is poison resistance granting advantage to saves against poison. The player will just roll with advantage, the same way they would if they had it for any other reason.

Info will probably never be referenced again after character creation. Traits will be shown as is on the character sheet in the appropriate racial traits section.

Info formats directly with ansi() calls. Traits use a handler to parse a text list with ~ and \| delimiters.

I mentioned some of this in [Naming and Calling Attributes]({% post_url 2019-04-10-naming-and-calling-attributes %}) and I still haven't come to a decision on which method is best, but I am leaning toward using the trait handler for everything. I think it would also handle skills well.

Another thing that occurred to me as I was creating the data dictonaries is that there is a lot of repetition. Darkvision is called a lot. Maybe it would be better to make a trait dictonary.

The pseudocode could look something like this:
```
&_5E.DARKVISION Trait Dictionary=Darkvision text.
&_5E.SUPERIOR_DARKVISION Trait Dictionary=More text.
&_5E.GNOME_SIZE Trait Dictionary=Gnomes are Medium creatures.

&_5E.RACE_GNOME here=Darkvision|Gnome_Size|Etc.
```

That's really rough, but it could iterate that race, match the attributes in the trait dictionary, and then pass them into the handler to render them. 

This is all kind of pointless once the base races have been created, but I'm sort of looking at it like a flag system. It would make adding new/custom races easier and allow for some interesting code if you wanted to see what traits are currently affecting your character. Drink a Potion of Night Sight and gain the darkvision flag, for instance. 