#[barfas, `|/`, %brfs](#brfs)

Door with tile

`|/` is a synthetic hoon that produces a [`%gold`]() [door]() with arms `q` and sample `[%bctr p]`. `|/` takes an associative list of names, [++term](), and expressions [++foot](), each pair of which is called an arm. The list must be closed with a `--`. `|/` is similar to `|_`, but defines a tile to be used by its arms rather than a sample.

##See also

`|_`

##Produces

Twig: `[%brfs p=tile q=(map term foot)]`

##Sample

`p` is a tile.
`q` is a [`map`]() with [`++term`]() keys and [`++foot`]() values.

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

    /~zod/try=> =kot
                  |/  a=(list)
                  +-  hed  -.a
                  +-  tal  +.a
                  --
    /~zod/try=> ~(hed kot "abc")
    i=~~a
    /~zod/try=> ~(tal kot ((list ,@ux) "abc"))
    t=~[0x62 0x63]
    /~zod/try=> =kom
                  |_  a=(list)
                  ++  hed  -.a
                  ++  tal  +.a
                  --
    /~zod/try=> ~(hed kom "abc")
    i=97
    /~zod/try=> ~(tal kom ((list ,@ux) "abc"))
    t=~[98 99]

This example is intended to show the difference between `|/` and `|_`. In both cases we create a door that takes a list, and implements two arms. One arm produces the head of the list, `+-  hed  -.a` and one the tail, `+-  tal  +.a`. When we call our `hed` function inside `|/` our type information is retained, and `i=~~a` is produced. Using `|_` we simply get `i=97`. `97` is the ASCII code for `a`. 

    ++  by                                                  ::  map engine
          ~/  %by
          |/  a=(map)
          ::
          +-  all
          ~/  %all
          |*  b=$+(* ?)
          |-  ^-  ?
          ?@  a
            &
          ?&((b q.n.a) $(a l.a) $(a r.a))

All of the container engines in `hoon.hoon` use `|/` to set up the tile for their operations. In `++by`, the map engine, `|/` creates a door that takes a map that is passed to its arms. See more about using `++by` in the [library]().