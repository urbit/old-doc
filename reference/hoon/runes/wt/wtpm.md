#[wutpam, `?&`, %wtpm](#wtpm)

[Short description]

#Syntax

`?&`, `wutpam`, `[%wtpm p=tusk]` is a synthetic hoon that
computes the "and" of the loobeans in `p`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

?&  i.p
        i.t.p
        i.t.t.p
    ==

##Wide form

?&(i.p i.t.p i.t.t.p)

##Irregular form

&(i.p i.t.p i.t.t.p)

##Examples

    1
    ~zod/try=> ?&(& &)
    %.y
    ~zod/try=> &(& &)
    %.y
    ~zod/try=> &(& |)
    %.n
    ~zod/try=> &((gth 2 1) |)
    %.n
    ~zod/try=> &((gth 2 1) &)
    %.y
