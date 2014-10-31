#[wutpat, `?@`, %wtpt](#wtpt)

[Short description]

#Syntax

`?@`, `wutpat`, `[%wtpt p=wing q=twig r=twig]` is a synthetic hoon 
that produces `q` if `p` is an atom, `r` otherwise.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

Kingside:

    ?@  p
      q
    r

##Wide form

?@(p q r)

##Irregular form

None

##Examples

    ~zod/try=> ?@(~ 1 2)
    ! mint-vain
    ! exit
    ~zod/try=> ?@(%ha 1 2)
    1
    ~zod/try=> ?@("" 1 2)
    1
    ~zod/try=> ?@("a" 1 2)
    2
    ~zod/try=> ?@([1 1] 1 2)
    ! mint-vain
    ! exit
    ~zod/try=> ?@(`*`[1 1] 1 2)
    2 
