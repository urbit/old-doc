#[dotlus, `.+`, %dtls](#dtls)

[Short description]

#Syntax

`.+`, `dotlus`, `[%dtls p=twig]` is a natural hoon that generates
nock operator `4`, which increments an atomic operand.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

.+  p

##Wide form

.+(p)

##Irregular form

+(p)

##Examples


    ~zod/try=> +(6)
    7
    ~zod/try=> +(2)
    3
    ~zod/try=> +(~zod)
    1
    ~zod/try=> +(0xff)
    256
    ~zod/try=> +(41)
    42
    ~zod/try=> +([1 2])
    ! type-fail
    ! exit
