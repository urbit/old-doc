##Overview

The `$` runes construct [`++tile`]()s. [`++tile`]()s are one of our primary building blocks in hoon, they define how we reduce our ASTs into well typed nouns that nock can compute. You can think of a [`++tile`]() sort of like a typeclass in Haskell.

##[`$?`]()
##[`$|`]()
##[`$&`]()
Forks: [`++tile`]()s that can be one of two things.

##[`$:`]()
##[`$=`]()
Tuples: unlabelled arrays, and tuples with [`++face`]s(), respectively.

##[`$*`]()
##[`$,`]()
##[`$@`]()
Reductions: [bunt](), [clam](), and [whip](), respectively. Tile reductions are important convenience methods for working with tiles, and are very broadly used.