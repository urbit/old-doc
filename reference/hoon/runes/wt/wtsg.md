#[wutsig, `?~`, %wtsg](#wtsg)

[Short description]

#Syntax

`?~`, `wutsig`, `[%wtsg p=wing q=twig r=twig]` is a synthetic hoon 
that produces `q` if `p` is `~`, `r` otherwise.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

?~  p
      q
    r

##Wide form

?~(p q r)

##Irregular form

None

##Examples

    ~zod/try=> ?~('a' 1 2)
    2
    ~zod/try=> ?~('' 1 2)
    1
    ~zod/try=> ?~(~zod 1 2)
    1
    ~zod/try=> ?~((sub 20 20) 1 2)
    1
