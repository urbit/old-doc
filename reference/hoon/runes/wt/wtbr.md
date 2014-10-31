#[wutbar, `?|`, %wtbr](#wtbr)

[Short description]

#Syntax

`?|`, `wutbar`, `[%wtbr p=tusk]` is a synthetic hoon that
computes the "or" of the loobeans in `p`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

?|  i.p
        i.t.p
        i.t.t.p
    ==

##Wide form

?|(i.p i.t.p i.t.t.p)

##Irregular form

|(i.p i.t.p i.t.t.p)

##Examples

    ~zod/try=> ?|(& |)
    %.y
    ~zod/try=> |(& |)
    %.y
    ~zod/try=> |(| |)
    %.n
    ~zod/try=> (gth 2 1)
    %.y
    ~zod/try=> |((gth 2 1) |)
    %.y
    ~zod/try=> |((gth 1 2) |)
    %.n
    ~zod/try=> |((gth 2 1) &)
    %.y
    ~zod/try=> |((gth 1 2) &)
    %.y
