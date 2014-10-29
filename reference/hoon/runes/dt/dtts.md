#[dottis, `.=`, %dtts](#dtts)

[Short description]

#Syntax

`.=`, `dottis`, `[%dtts p=twig q=twig]`is a natural hoon that applies nock 5 (equals) to determine if the products of p and q are equivalent.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

.=  p
        q

##Wide form

.=(p q)

##Irregular form

=(p q)

##Examples

    ~zod/try=> =(0 ~)
    %.y
    ~zod/try=> =(1 2)
    %.n
    ~zod/try=> =(" " [32 0])
    %.y
    ~zod/try=> =(~nec 1)
    %.y
    ~zod/try=> =([%a 2] a/(dec 3))
    %.y
    ~zod/try=> =([%b 2] a/(dec 3))
    %.n
