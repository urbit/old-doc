#[barfas, `|/`, %brfs](#brfs)

`|/`, `barfas`, `[%brfs p=tile q=(map term foot)]` is a synthetic hoon
that produces a vulcanized `%gold` door with arms `q`, sample `[%bctr p]`.

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


In ++by, |/ creates a door that takes a map that is passed to its arms, designated with `+-`, since the arms of `|/` are wet.

See also `|_`

    /~zod/try=> =kot
                  |/  a=(list)
                  +-  hed  -.a
                  +-  tal  +.a
                  --
    /~zod/try=> ~(hed kot "abc")
    i=~~a
    /~zod/try=> ~(tal kot ((list ,@ux) "abc"))
    t=~[0x62 0x63]
    
Compare

    /~zod/try=> =kom
                  |_  a=(list)
                  ++  hed  -.a
                  ++  tal  +.a
                  --
    /~zod/try=> ~(hed kom "abc")
    i=97
    /~zod/try=> ~(tal kom ((list ,@ux) "abc"))
    t=~[98 99]
