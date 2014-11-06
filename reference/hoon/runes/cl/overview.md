##Overview

The `:` runes construct [tuples]().

There is no natural `:` rune. Instead, all of them derive from the autocons property of `++twig`, as show below.

++  twig  $&  [p=twig q=twig]

Namely, a cell of two twigs is a twig producing a cell of the results of the two original sub-twigs.

Notable `;` runes:

-`:-` creates a tuple of two elements `p` and `q`.

-`:+` creates a tuple of three elements `p`, `q`, and `r`.

-`:^` creates a tuple of four elements `p`, `q`, `r`, and `s`.

-`:*` creates a tuple n elements.

-`:~` creates a null terminated tuple of n elements.
