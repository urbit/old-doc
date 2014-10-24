#[centis, `%=`, %cnts](#cnts)

Evaluate with changes

`%=` is a natural hoon thatevaluates `p` with the changes specified in `q`. `%=` is used to change a batch of [wing]()s inside a [`++wing`]() all at once, ensuring that the product is type checked.

##See also

`%_`

##Produces

Twig: `[%cnts p=wing q=tram]`

##Sample

`p` is a [++wing]().
`q` is a [++tram]().

##Tall form

    %=  p
          p.i.q    q.i.q
          p.i.t.q  q.i.t.q
        ==

##Wide form

    %=(p p.i.q q.i.q, p.i.t.q q.i.t.q)

##Irregular form

    p(p.i.q q.i.q, p.i.t.q q.i.t.q)

##Examples

    /~zod/try=> =+  a=[p=5 q=6]
                a(p 2)
    [p=2 q=6]
    /~zod/try=> =+  a=[p=5 q=6]
                a(q 'c')
    [p=5 q='c']
