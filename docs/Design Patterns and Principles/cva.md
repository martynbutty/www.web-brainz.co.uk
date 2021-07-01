---
title: Commonality Variability Analysis
---
A principle of good software design is to separate things that change from those that do not. Commonality variability 
analysis is a way of achieving this.

### Benefits

Commonality variability analysis helps us to focus on interfaces and stop us from looking at implementation too soon. 
It leads us to hide the implementation by focussing on the abstractions first. It encourages us to look at the high and 
low level aspects of design, but separately. It helps us to design by contract, thus creating an architecture that is more testable.

### Commonality Analysis

This is the search for common elements that help us understand how members are the same. They are:

*   Recognised from experience - e.g. lots of different species of tree have the commonality of being a tree.
*   Deduced through analysis (abstracted) - e.g. pens are writing instruments made from plastic, have caps, same shape etc.

The commonalities define the basic concepts in a problem domain. Avoid thinking just in terms of data or function, 
for example, a pen and a book may be classed as common because they are used for teaching/communication, or are both portable.

### Variability Analysis

This is the next step after deciding on a commonality. It should be done within the context of the commonality by asking, 
how do these things vary. Using an example of different kinds of pen, if the commonality is "writing instrument", then 
the variability's might be what they can write on and line thickness etc. However, if the commonality is "plastic things", 
then the previous variability's don't apply and instead we should have variability's like type of plastic and amount of plastic.

In the case of the "writing instrument" commonality, a (traditional) pencil would plug in to this model. However it would 
not plug in to the "plastic things" commonality. Therefore if you know that you want to extend your commonality to include 
pencils, then "plastic things" is probably not the correct commonality.

### Tips

*   When looking at something within the problem domain, ask yourself is it a particular way of doing something (a variation), 
    or is it a concept (a way of conceptually thinking about different ways of doing things) (commonality).
*   If something is a variability, what is it a variation of? this becomes the base class or interface.
*   If something is a commonality, then it is a base class or interface - think about the different ways in which it can vary.
*   If something is neither a commonality or variability, it may be just a stand-alone function. Identify this as a 
    probable object and consider if this should have an interface to hide it, or if it should be dealt with concretely.

You are looking for the "is-a" relationships. Other relationships such as "uses", "contains", "builds" or "knows-of", 
and grouping things just because they go together are not a part of commonality variability analysis. These are what 
design patterns are concerned with, so these relationships should be dealt with later to avoid prematurely coupling objects.

Not all commonalities are useful, so don't be afraid to discard some.
