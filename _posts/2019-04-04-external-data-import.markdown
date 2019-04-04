---
layout: post
title:  External Data Import
date:   2019-04-04 07:10
categories: systems
---
I need to figure out how to import data from external sources into the game. I think there is some code at https://github.com/thenomain/Mu--Support-Systems/tree/master/Weather I can look at. A cursory look suggests it is using a site's API to download a copy of a file, chop it up, and serve it out as help file. This is brilliant.

I don't care about weather so much as I care about things like news headlines, stock prices, and sports scores. I suspect all of this will contain fewer fields but keep a larger buffer of data. The weather seems to be live--that is, it downloads new data whenever cron runs and that is _the_ data. So, I may need to look for a way to save multiple entries in the source file or in attributes.

What I have in mind is actually recording live sports scores but assigning them to fictional entities and then allowing characters to place wagers on the outcome.

Maybe Pathfinder doesn't have baseball, but what about horse racing? Hockey might work for some sort of magical dodgeball. There's probably even a way to use basketball.

Real world currency exchange rates could inform the value of precious gems. I wouldn't ever consider debasing the copper/silver/gold/platinum exchange, but if you tie the USD/Yen exchange rate to gold/rubies you could do something interesting.

Consider the following pseudocode:
```
@create Ruby Ring
@desc Ruby Ring=A gold ring with a huge ruby set into a dragon's claw.
&material Ruby Ring=ruby
&material-quantity Ruby Ring=2
&value Ruby Ring=lookup material * material-quantity
```
Say you have an exchange rate of 1 USD to 110 Yen. It does some math, but that ring is worth 220 gp now. Say the Yen grows stronger and becomes 1:100, the ring devalues a little. It sort of fakes an economy with very little effort and might encourage an interesting hoarding tendency in the players. Wouldn't it be cool to have an actual room of treasure?