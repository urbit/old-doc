#[centis, `%=`, %cnts](#cnts)

Evaluate with changes

`%=` is a natural hoon that evaluates `p` with the changes specified in `q`. `%=` is used to specify changes in the context of `p`.

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



