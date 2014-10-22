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

The common action performed on a trap is kicking it: pulling arm `$`. A `%-` 
with no arguments performs a kick.

    ~zod/try=> |.(42)
    < 1.pnv
      [[[@da @ta] [@p @ta] *''] @n <250.yum 41.int 414.hhh 100.xkc 1.ypj %164>]
    >
    ~zod/try=> $:|.(42)
    42
    ~zod/try=> =a |.(~&(%hi 7))
    ~zod/try=> (a)
    %hi
    7
