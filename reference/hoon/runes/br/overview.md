##Overview

The `|` runes construct [core]()s. In the broadest case you can think of a core as similar to an object with named properties that can contain either functions or data. hoon also defines special cases of [core]()s for common operations, functions, functions called by default, and so on.

##[`|%`]() 
The natural `|` rune. `|%` builds a core using a list of [`++arm`]()s, which generally contain [`++twig`]()s.

##[`|=`]()
##[`|*`]()
Gates. A gate is a core with one arm [`$`], the empty name and which takes a sample `p`. `|=` creates a `dry` gate, where the sample is typechecked at compile time. `|*` creates a `wet` gate, where the sample is typechecked at runtime against its product type. 

##[`|-`]()
##[`|.`]()
Traps. Both reduce to a `|%` with one arm `$`, the empty name. We use `|.` to put some computation into a wrapper, which we call a "trap". `|-` is identical to `|.` except for that it is automatically kicked after construction.
