#[tisgar, `=>`, %tsgr](#tsgr)

[Short description]

#Syntax

`=>`, `tisgar`, `[%tsgr p=twig q=twig]` is a natural hoon that
uses the product of `p` as the subject of `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

=>  p
    q

##Wide form

=>(p q)

##Irregular form

=>(p q)

##Examples

    ~zod/try=> =>("ham" -)
    i=~~h
    ~zod/try=> =>((add 2 4) [. .])
    [6 6]
    ~zod/try=> =>((add 2 4) [. %ha])
    [6 %ha]
