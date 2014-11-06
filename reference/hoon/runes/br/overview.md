##Overview

The `|` runes construct [cores](). A core is similar to an object with named properties that can contain either functions or data. 

`|%` is the natural `|` rune. It builds a core using a list of [`++arm`]()s, which generally contain [`++twig`]()s.

Other notable `|` runes:

-`|.` reduces to a `|%` with one arm `$`, the empty name. We use `|.` to put a [`++twig`]() into a wrapper, called a trap.

-`|-` is identical to `|.` except for that it is automatically kicked after construction.

-`|=` creates a `dry` [gate](), which is a core with one arm [`$`], the empty name. It is different from `|.` and `|-` in that it has a [sample](), from which the output type is computed.

-`|*` is a synthetic rune that is used to create a `wet` [gate](), whose output type is computed from the type of the actual (as opposed to formal) sample.
