#[ketlus, `^+`, %ktls](#ktls)

[Short description]

#Syntax

`^+`, `ketlus`, `[%ktls p=twig q=twig]` is a natural hoon that casts the product of `q` to the type of `p`, verifying that it contains the type of `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

^+  p
        q

##Wide form

^+(p q)

##Irregular form

None

##Examples

    ~zod/try=> (add 90 7)
    97
    ~zod/try=> ^+('cord' (add 90 7))
    'a'

