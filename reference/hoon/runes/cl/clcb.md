#[colcab, `:_`, %clcb](#clcb)

[Short description]

#Syntax

`:_`, `colcab`, `[%clcb p=twig q=twig]` is a synthetic hoon that
produces the cell `[q p]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

:_  p
    q

##Wide form

:_(p q)

##Irregular form

undefined

##Examples

    ~zod/try=> :_(1 2)
    [2 1]
    ~zod/try=> `tape`:_(~ 'a')
    "a"
