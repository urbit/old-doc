#[wutgar, `?>`, %wtgr](#wtgr)

[Short description]

#Syntax

`?>`, `wutgar`, `[%wtgr p=twig q=twig]` is a synthetic hoon that
produces `q`, asserting that `p` is yes (`&`, 0).

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

?>  p
        q

##Wide form

?>(p q)

##Irregular form

None

##Examples


    ~zod/try=> ?>(=(0x1 1) %foo)
    %foo
    ~zod/try=> ?>(=(0x1 0) %foo)
    ! exit
