#[kethep, `^-`, %kthp](#kthp)

[Short description]

#Syntax

`^-`, `kethep`, `[%kthp p=tile q=twig]` is a synthetic hoon that casts `q` to `~(bunt al p)`, ie, the icon of `p`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

^-  p
        q

##Wide form

^-(p q)

##Irregular form

`p`q

##Examples

    ~zod/try=> (add 90 7)
    97
    ~zod/try=> `@t`(add 90 7)
    'a'
    ~zod/try=> ^-(@t (add 90 7))
    'a'

