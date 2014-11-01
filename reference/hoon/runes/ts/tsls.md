#[tislus, `=+`, %tsls](#tsls)

[Short description]

#Syntax

`=+`, `tislus`, `[%tsls p=twig q=twig]` is a synthetic hoon that
pushes `p` on the subject and sends it to `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

=+  p
    q

##Wide form

=+(p q)

##Irregular form

None

##Examples

    ~zod/try=> =+(a=1 =+(b=(add 10 a) [a b]))
    [1 11]
    ~zod/try=> .*(. =+(a=1 =+(b=(add 10 a) [a b])))
    11

