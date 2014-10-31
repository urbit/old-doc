#[wutket, `?^`, %wtkt](#wtkt)

[Short description]

#Syntax

`?^`, `wutket`, `[%wtkt p=wing q=twig r=twig]` is a synthetic hoon
that evaluates `r` if `p` is equal to the bunt for its tile, otherwise
`q` is evaluated.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

?^  p
      q
    r

##Wide form

?^(p q r)

##Irregular form

None

##Examples

    ~zod/try=> ?^  ""
                 %full
               %empty
    %empty
    ~zod/try=> ?^  "asd"
                 %full
               %empty
    %full
    ~zod/try=> ?^  `(unit)`~
                 %full
               %empty
    %empty
    ~zod/try=> ?^  `(unit)`[~ u=20]
                 %full
               %empty
    %full
