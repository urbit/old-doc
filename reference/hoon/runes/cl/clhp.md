#[colhep, `:-`, %clhp](#clhp)

Cell

`:-`, `colhep`, `[%clhp p=twig q=twig]` is a synthetic rune that
produces the cell `[p q]`.

##Produces

Twig: `[%clhp p=twig q=twig]`

##Sample

`p` is a [twig]().
`q` is a [twig]().

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

This is the most straightforward case of `:-`, producing a cell of static data in either tall or wide form.

    /~zod/try=> 
        :-  (add 2 2)
        |-  (div 4 2)
    [4 2]

Most commonly `:-` helps to organize code, allowing you to produce a cell from nested computation.