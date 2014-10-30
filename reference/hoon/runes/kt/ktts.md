#[kettis, `^=`, %ktts](#ktts)

[Short description]

#Syntax

`^=`, `kettis`, `[%ktts p=toga q=twig]` is a natural hoon that wraps `q` in the toga `p`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

^=  a

##Wide form

^=(a)

##Irregular form

None

##Examples

    ~zod/try=> a=1
    a=1
    ~zod/try=> ^=  a
               20
    a=20
    ~zod/try=> [b ~ c]=[1 2 3 4]
    [b=1 2 c=[3 4]]
    ~zod/try=> (ream 'mol=ham')
    [%ktts p=p=%mol q=[%cnzz p=~[%ham]]]
    ~zod/try=> (ream '[a b]=.')
    [%ktts p=[%2 p=p=%a q=p=%b] q=[%cnts p=~[[%.y p=1]] q=~]]
