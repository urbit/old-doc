#[bartar, `|*`, %brtr](#brtr)

[Short description]

#Syntax

`|*`, `bartar`, `[%brtr p=tile q=twig]` is a synthetic hoon that
produces a vulcanized wet gate with arm `q`, sample `[%bctr p]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|*  p
    q

##Wide form

|*(p q)

##Irregular form

None

##Examples

++  flop                                                ::  reverse
      ~/  %flop
      |*  a=(list)
      =>  .(a (homo a))
      ^+  a
      =+  b=`_a`~
      |-
      ?@  a
        b
      $(a t.a, b [i.a b])

In ++flop, `|*` creates a wet gate that takes a ++list (link).

