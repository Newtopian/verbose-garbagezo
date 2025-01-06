# About Code
Various shit about code ... or just stuff about how I experience the giant heap of garbage and the occasionnal diamond in the rough I write and read while coding.


# The Fear Factor
That has to be the one thing I can summarise how I tackle systems, write code or view how I'd like it to be.
Systems we write get complicated... fast... and we rapidly come to a point where we will need to iterate on 
these systems.  
And here I think the number one ennemy, the primordial gut wrenching, sweat inducing, shit your pants thing that
grips you is...  Ho Shit...  I gotta change that code !!!

![Ho shit ... I gotta change that code !](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExM2Z0aXNtcTR0eHA3ZzJzb2hkN2g0eHN3YTBreXd1a2E4azE1YzdrMiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/a79Jr229u3bzO/giphy.gif)

If you feel that way, then you never _truly_ thought about your future self when you first wrote that system.

Why all the self hate !

In short, before design patterns, or lack thereof, before architecture, before use-cases or requirements gathering...
the ONE thing you should keep in mind thoughout the process... is ... how will you manage the fear factor.

As you ponder on how to optimize this or make this a nicer piece of code...  you should think of your future self and
think on how you can keep this fear down.

THAT is why we do layers of abstractions, is why we create these architectures, why we do design patterns.  That is 
why we automate the shit out of everything we can, you want to manage the dread that will innevitably come greet
you the next time you need to interact with this code / system.

* How easy it is to experiment with it ?
* How damaging are errors and mistakes ?  In prod ?
* And should you fuck things up, I mean REALLY fuck things up... how easy, and fast it is to get back to a known good baseline ?

I mean think of the ABSOLUTE worst case scenario and use that as the starting point to find a really _really_ vicious, sadistic way you can immolate the 
system you are working in, where _nuking_ it would be a mercy...

Typically this would entice two responses, either you curl up in fetal position and then try and learn this by heart for the next time :

> "I must not fear.
> Fear is the mind-killer.
> Fear is the little-death that brings total obliteration.
> I will face my fear.
> I will permit it to pass over me and through me.
> And when it has gone past, I will turn the inner eye to see its path.
> Where the fear has gone there will be nothing. Only I will remain."

OR

You look at this image and without a hint of sarcasm truly feel zen cause you KNOW how to fix this, fast and easy !  Aint nothing the univese can throw at you that will not make you finish this cup of tea before getting the situation under control.

![it's fine](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExeGpzOTF1ZDkyYWYyMDk0NmYzcGtzODB4enA5azdmYXBrM21ueTluNSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/NTur7XlVDUdqM/giphy.gif)

The biggest wins I've made were not so much that super algorithm, or how I made this bit super efficient.  But how
I got a manually, error prone, and non-resilient process that would take hours (weeks in one case) down to mere minutes but most of all...

A brain dead operation you could confidently do very drunk while still at a bar with just your cell-phone to interact with the system. (literally a true story... for another time)

In short, how I reduced the fear factor down to a point where making mistakes was just part of work, it was allowed, it was accepted as unavoidable and thus could be addressed rapidly and/or could be isolated easily such that experiments did not affect normal workflows.

Dont try and manage fear, just remove it's root cause !

Keep that in check, everything ideas or requests get answered along these lines :

> gimme an hour or so I'll try something up see how far we can take this idea.
