#[colsig, `:~`, %clsg](#clsg)

[Short description]

#Syntax

`:~`, `colsig`, `[%clsg p=tusk]` is a synthetic hoon that
produces a null-terminated tuple.

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

:~(i.p i.t.p i.t.t.p)

##Irregular form

~[i.p i.t.p i.t.t.p]

##Examples

    /~zod/try=> :~(5 3 4 2 1)
    [5 3 4 2 1 ~]
    /~zod/try=> ~[5 3 4 2 1]
    [5 3 4 2 1 ~]
    /~zod/try=> :~  5
                    3
                    4
                    2
                    1
                ==
    [5 3 4 2 1 ~]

