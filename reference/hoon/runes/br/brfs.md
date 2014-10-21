#[barfas, `|/`, %brfs](#brfs)

`|/`, `barfas`, `[%brfs p=tile q=(map term foot)]` is a synthetic hoon
that produces a vulcanized `%gold` tray with arms `q`, sample `[%bctr p]`.

[Short description]

undefined

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|/  p
      +-  p.n.q
        q.n.q
      --

##Wide form

None

##Irregular form

None

##Examples

++  by                                                  ::  map engine
      ~/  %by
      |/  a=(map)

      +-  all
      ~/  %all
      |*  b=$+(* ?)
      |-  ^-  ?
      ?@  a
        &
      ?&((b q.n.a) $(a l.a) $(a r.a))


In ++by, |/ creates a tray that takes a map that is passed to its arms, designated with `+-`, since the arms of `|/` are wet.

