#[collus, `:+`, %clls](#clls)

[Short description]

#Syntax

`:+`, `collus`, `[%clls p=twig q=twig r=twig]` is a synthetic hoon that
produces a cell `[p q r]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

Kingside:

    :+  p
      q
    r

Queenside:

    :+  p   q
    r

##Wide form

:+(p q r)

##Irregular form

undefined

##Examples

    /~zod/try=> :+  1
                  2
                3
    [1 2 3]
    /~zod/try=> :+(%a ~ 'b')
    [%a ~ 'b']
