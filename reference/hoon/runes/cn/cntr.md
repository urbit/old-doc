#[centar, `%*`, %cntr](#cntr)

Pull with changes

`%*` is a synthetic rune that [pull]()s the wing `p` from a [door]() `q` with changes `r`. `%*` is used to specify changes in the context of a wing when it is pulled.

##Produces

Twig: `[%cntr p=wing q=twig r=tram]`

##Sample

`p` is a [++wing]().
`q` is a [++twig]().
`r` is a [++tram]().

##Tall form

    %*  p  q
      p.i.r  q.i.r
      p.i.t.r  q.i.t.r
    ==

##Wide form

    %*(p q p.i.r q.i.r, p.i.t.r q.i.t.r)

##Irregular form

None

##Examples



