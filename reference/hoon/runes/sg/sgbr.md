#[sigbar, `~|`, %sgbr](#sgbr)

[Short description]

#Syntax

`~|`, `sigbar`, `[%sgbr p=twig q=twig]` is a synthetic hoon that
presents the product of `p` in the stack trace if `q` crashes.
The computation is only performed if needed.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

~|  p
        q

##Wide form

^|(p q)

##Irregular form

None

##Examples



