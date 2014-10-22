#[barlus, `|+`, %brls](#brls)

[Short description]

#Syntax

`|+`, `barlus`, `[%brls p=tile q=twig]` is a synthetic hoon that
produces a dry `%iron` gate with arm `q`, sample `[%bctr p]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|+  p
    q

##Wide form

|+(p q)

##Irregular form

None

##Examples


    ~zod/try=> +<:|+(a=@ a)
    ! -axis.6
    ! peek-park
    ! exit
    ~zod/try=> +<:|=(a=@ a)
    a=0
    ~zod/try=> %.(20 |+(a=@ a))
    20
    ~zod/try=> %.(20 |+(a=@ (add a 12)))
    32

An `iron` gate is like a `gold` gate, but cannot have its sample read, only
written.
