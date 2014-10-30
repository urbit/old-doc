#[haxgar, `#>`, %hxgr](#hxgr)

[Short description]

#Syntax

`#>`, `haxgar`, `[%hxgr p=tusk]`is a synthetic hoon that
slams the assumed gate `cain` on `[%zpgr %cntr p]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

?

##Wide form

?

##Irregular form

    <i.p i.t.p i.t.t.p>

##Examples
    
    ~zod/try=/zop> >1<
    [%leaf p="1"]
    ~zod/try=/zop> >`path`"abc"<
    [%rose p=[p="/" q="/" r=""] q=~[[%leaf p="a"] [%leaf p="b"] [%leaf p="c"]]]
    ~zod/try=/zop> >0x5 ~zod 'a'<
    [ %rose
      p=[p=" " q="[" r="]"]
      q=~[[%leaf p="0x5"] [%leaf p="~zod"] [%leaf p="'a'"]]
    ]
    ~zod/try=/zop> >|.(1)<
    [ %rose
      p=[p=" " q="<" r=">"]
        q
      ~[
        [%leaf p="1.gcq"]
        [ %rose
          p=[p=" " q="[" r="]"]
            q
          ~[
            [%leaf p="@n"]
            [ %rose
              p=[p=" " q="<" r=">"]
                q
              ~[
                [%leaf p="250.xnq"]
                [%leaf p="41.vrk"]
                [%leaf p="418.ssa"]
                [%leaf p="101.jzo"]
                [%leaf p="1.ypj"]
                [%leaf p="%164"]
              ]
            ]
          ]
        ]
      ]
    ]
