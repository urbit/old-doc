#[zapgar, `!>`, %zpgr](#zpgr)

[Short description]

#Syntax

`!>`, `zapgar`, `[%zpgr p=twig]` is a synthetic hoon that
produces a vase (a [type noun] cell) with the value `p`.

Uses biblical arms `onan`, `abel`

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

!>  p

##Wide form

!>(p)

##Irregular form

None

##Examples

    ~zod/try=> !>(1)
    [p=[%atom p=%ud] q=1]
    ~zod/try=> !>(~zod)
    [p=[%atom p=%p] q=0]
    ~zod/try=> !>([1 2])
    [p=[%cell p=[%atom p=%ud] q=[%atom p=%ud]] q=[1 2]]
    ~zod/try=> !>([|.(20)]:~)
    [   p
      [ %core
        p=[%cube p=0 q=[%atom p=%n]]
          q
        [ p=%gold
          q=[%cube p=0 q=[%atom p=%n]]
          r=[p=[1 20] q={[p=%$ q=[%ash p=[%dtzy p=%ud q=20]]]}]
        ]
      ]
      q=[[1 20] 0]
    ]
