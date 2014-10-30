#[tisbar, `=|`, %tsbr](#tsbr)

[Short description]

#Syntax

`=|`, `tisbar`, `[%tsbr p=tile q=twig]` is a synthetic hoon that
pushes `~(bunt al p)` on the subject and sends it to `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

=|  p
        q

##Wide form

=|(p q)

##Irregular form

None

##Examples

    ~zod/try=> =|(a=^ a)
    [0 0]
    ~zod/try=> =|(a=@p a)
    ~zod
