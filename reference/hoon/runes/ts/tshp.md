#[tishep, `=-`, %tshp](#tshp)

[Short description]

#Syntax

`=-`, `tishep`, `[%tshp p=twig q=twig]` is a synthetic hoon that
pushes `q` on the subject and sends it to `p`.

See also: `=+`

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

=-  p
    q

##Wide form

=-(p q)

##Irregular form

None

##Examples


    ~zod/try=> =-  [%a (add 10 -)]
               %-  lent
               ~[0 1 2 3 4]
    [%a 15]
