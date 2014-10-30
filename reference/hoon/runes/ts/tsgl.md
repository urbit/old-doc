#[tisgal, `=<`, %tsgl](#tsgl)

[Short description]

#Syntax

`=<`, `tisgal`, `[%tsgl p=twig q=twig]` is a synthetic hoon that
uses the product of `q` as the subject of `p`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

=<  p
    q

##Wide form

=<(p q)

##Irregular form

p:q

##Examples

    ~zod/try=> b:[a=1 b=2 c=3]
    2
    ~zod/try=> =<  lom
               |%
               ++  lom  (add 2 tak)
               ++  tak  4
               --
    6

