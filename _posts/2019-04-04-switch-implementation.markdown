---
layout: post
title:  Switch() Implementation
date:   2019-04-04 10:43
categories: mushcode functions
---
I wanted to follow up on what implementing switch() into a @description to make a phased or state-based room looks like. This will probably be really important later with different kind of vision modes. Consider what a candlelit room might look like to someone with normal vision, low-light vision, and darkvision.

I identified three attributes that I needed to pay attention to:
* _PF.STATLOCK - This is set once attribute choices are finalized by the validate command. If this is set, the player will only see a description showing what the final choices are.
* _PF.ROLLED? - Has the player rolled yet?
* _PF.ARRAYCHOICE - Has the player chosen to keep their roll or go with a default array of attribute scores?

I was pretty sure I knew what I needed to set the switch statement to, but I needed to test it so I put the following at the bottom of the description of the room so I could see it in each phase with the existing evaluation heavy code:

```
[hasattr(%#,_PF.STATLOCK)]|[hasattr(%#,_PF.ROLLED?)]|[hasattr(%#,_PF.ARRAYCHOICE)]
```

The tests matched my expectations and am using the following switch criteria:
* 0 0 * = Shouldn't be possible to have _PF.ARRAYCHOICE before, but even if you do, it isn't important. In the test, this was 0 0 0.
* 0 1 0 = Rolled, but haven't made a choice yet. This has to be explicit.
* 0 1 1 = Rolled, and made a choice. This has to be explicit.
* 1 * * = CMD-VALIDATE should prevent _PF.STATLOCK from being true while the other two are not. The reason I don't care about the latter two entries is the edge case where this is done by a wizard. In the test, this was 1 1 1.

Here is a snip of the description:

```
[switch([hasattr(%#,_PF.STATLOCK)]|[hasattr(%#,_PF.ROLLED?)]|[hasattr(%#,_PF.ARRAYCHOICE)],
0|0|*,{Make a roll},
0|1|0,{Choose an array},
0|1|1,{Assign attributes},
1|*|*,{Final stats},
{})]
```

That last {} is just the default case. It looks like I have to set it or it will consider anything that doesn't match the default case. In this instance, it would work, but it is 3 characters so I left it in for form. I wound up only cutting the description length by 200 characters, but it evaluates significantly less often now.