#[coltar, `:*`, %cltr](#cltr)

[Short description]

#Syntax

`:*`, `coltar`, `[%cltr p=tusk]` is a synthetic hoon that
produces a tuple.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

:~  i.p
        i.t.p
        i.t.t.p
    ==

##Wide form

:*(i.p i.t.p i.t.t.p)

##Irregular form

[i.p i.t.p i.t.t.p]

##Examples

    /~zod/try=> [5 3 4 1 4 9 0 ~ 'a']
    [5 3 4 1 4 9 0 ~ 'a']
    /~zod/try=> :*(5 3 4 1 4 9 0 ~ 'a')
    [5 3 4 1 4 9 0 ~ 'a']
    /~zod/try=> :*  5
                    3
                    4 
                    1
                    4
                    9
                    0
                    ~
                    'a'
                ==
    [5 3 4 1 4 9 0 ~ 'a']
