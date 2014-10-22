#[colket, `:^`, %clkt](#clkt)

[Short description]

#Syntax

`:^`, `colket`, `[%clkt p=twig q=twig r=twig s=twig]` is a 
synthetic hoon that produces a cell `[p q r s]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

Kingside:

    :^    p
        q
      r
    s

Queenside:

    :^  p  q
      r
    s

    :^  p  q  r  
    s

##Wide form

:^(p q r s)

##Irregular form

undefined

##Examples

/~zod/try=> :^(1 2 3 4)
[1 2 3 4]
/~zod/try=> :^  5  6
              7
            8
[5 6 7 8]
