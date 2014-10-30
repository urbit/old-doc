#[semcol, `;:`, %smcl](#smcl)

[Short description]

#Syntax

`;:`, `semcol`, `[%smcl p=twig q=tusk]` is a synthetic hoon that
applies `p`, a binary gate, to the n-ary tuple `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

;:  p
      i.q
      i.t.q
      i.t.t.q
    ==

##Wide form

;:(p i.q i.t.q i.t.t.q)

##Irregular form

:(p i.q i.t.q i.t.t.q)

##Examples

    ~zod/try=> ;:(add 3 4 5)
    12
    ~zod/try=> :(add 3 4 5)
    12
    ~zod/try=> :(weld "foo" "bar" "baz")
    ~[~~f ~~o ~~o ~~b ~~a ~~r ~~b ~~a ~~z]
    ~zod/try=> `tape`:(weld "foo" "bar" "baz")
    "foobarbaz"
    ~zod/try=> `tape`(weld "foo" (weld "bar" "baz"))
    "foobarbaz"



