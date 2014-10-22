#[colhep, `:-`, %clhp](#clhp)

[Short description]

#Syntax

`:-`, `colhep`, `[%clhp p=twig q=twig]` is a synthetic hoon that
produces the cell `[p q]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

:-  p
    q

##Wide form

:-(p q)

##Irregular form

[p q]

##Examples

    ~zod/try=> :-(1 2)
    [1 2]
    ~zod/try=> :-  'a'
               %b
    ['a' %b]
    
Cell of two nouns
