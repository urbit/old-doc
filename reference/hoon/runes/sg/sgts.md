#[sigtis, `~=`, %sgts](#sgts)

[Short description]

#Syntax

`~=`, `sigtis`, `[%sgts p=twig q=twig]` is a synthetic hoon that
hints to the interpreter that `q` may produce a noun equal to the
already existing `p`, avoiding duplication.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

~=  p
        q

##Wide form

~=(p q)

##Irregular form

None

##Examples

    ~zod/try=> 20
    20
    ~zod/try=> =+(a=20 20)
    20
    ~zod/try=> =+(a=20 ~=(a 20))
    20
    ~zod/try=> (make '=+(a=20 20)')
    [%8 p=[%1 p=20] q=[%1 p=20]]
    ~zod/try=> (make '=+(a=20 ~=(a 20))')
    [%8 p=[%1 p=20] q=[%10 p=[p=1.836.213.607 q=[%0 p=2]] q=[%1 p=20]]]
    ~zod/try=> `@tas`1.836.213.607
    %germ
