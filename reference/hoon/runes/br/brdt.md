#[bardot, `|.`, %brdt](#brdt)

[Short description]

#Syntax

`|.`, `bardot`, `[%brdt p=twig]` is a synthetic hoon that produces
a dry `%gold` trap (cores, link). `|.` takes a twig.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|.  p

##Wide form

|.(p)

##Irregular form

None

##Examples

++  reel                                                ::  right fold
      ~/  %reel
      |*  [a=(list) b=_=|([p=* q=*] |.(q))]
      |-  ^+  q.b
      ?@  a
        q.b
      (b i.a $(a t.a))

In ++reel, `|.` is used to specify the body of the expression to right fold over a given list.

