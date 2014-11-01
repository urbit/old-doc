#[tisket, `=^`, %tskt](#tskt)

[Short description]

#Syntax

`=^`, `tisket`, `[%tskt p=twig q=twig r=twig s=twig]` is a synthetic 
hoon that handles a product which is a cell of a new result, and
a mutation to the subject.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

Kingside:

     =^    p 
        q
      r
    s

Queenside:

    =^  p  q
      r
    s

##Wide form

=^(p q r s)

##Irregular form

None

##Examples

    ~zod/try=> =+  a=3
               =^  b  a  [a +(a)]
               [a ~ b]
    [4 ~ 3]
    ~zod/try=> =+  a="ham"
               =^  b  a  a
               [<`@tas`b> a]
    ["%h" "am"]
