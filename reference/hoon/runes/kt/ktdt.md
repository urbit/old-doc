#[ketdot, `^.`, %ktdt](#ktdt)

[Short description]

#Syntax

`^.`, `ketdot`, `[%ktdt p=twig q=twig]` is a synthetic hoon that casts `q` to the type of `(p q)`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

^.  p
        q

##Wide form

None

##Irregular form

None

##Examples

    ~zod/try=> ~[1 2 3 4]
    [1 2 3 4 ~]
    ~zod/try=> ^.(limo ~[1 2 3 4])
    [i=1 t=[i=2 t=[i=3 t=[i=4 t=~]]]]

