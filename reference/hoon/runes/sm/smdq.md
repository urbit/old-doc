#[semdoq, %smdq](#smdq)

[Short description]

#Syntax

`semdoq`, `[%smdq p=(list beer)]` is a synthetic rune used to make strings, interpreted or not.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

None

##Wide form

None

##Irregular form

    "foo"

##Examples


    ~zod/try=> "foo"
    "foo"
    ~zod/try=> "bar"
    "bar"
    ~zod/try=> "ba{<+(2)>}r"
    "ba3r"
    ~zod/try=> (ream '"foo"')
    [%smdq p=~[102 111 111]]
    ~zod/try=> (ream '"ba{<+(2)>}r"')
    [ %smdq
      p=~[98 97 [~ p=[%cltr p=~[[%hxgl p=~[[%dtls p=[%dtzy p=%ud q=2]]]]]]] 114]
    ]
