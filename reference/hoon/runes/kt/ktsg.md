#[ketsig, `^~`, %ktsg](#ktsg)

[Short description]

#Syntax

`^~`, `ketsig`, `[%ktsg p=twig]` is a natural hoon that
tries to execute `p` statically at compile time; if this fails, `p` remains dynamic.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

^~  a

##Wide form

^~(a)

##Irregular form

None

##Examples

    ~zod/try=> (make '|.(42)')
    [p=[%1 p=[1 42]] q=[%0 p=1]]
    ~zod/try=> (make '$:|.(42)')
    [%8 p=[%1 p=[1 42]] q=[%9 p=2 q=[%0 p=1]]]
    ~zod/try=> (make '^~($:|.(42))')
    [%1 p=42]

