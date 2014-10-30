#[semsem, `;;`, %smsm](#smsm)

Slams q through gate p, asserting that the resulting noun .= the original, and producing it.

#Syntax

`;;`, `semsem`, `[%smsm p=twig q=twig]` is a synthetic hoon that
types `q` as a fixpoint of `p`.

See also: [hard]


##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

;;  p
        q

##Wide form

;;(p q)

##Irregular form

None

##Examples


    ~zod/try=> ^-(tape ~[97 98 99])
    ! type-fail
    ! exit
    ~zod/try=> ;;(tape ~[97 98 99])
    "abc"
    ~zod/try=> (tape [50 51 52])
    "23"
    ~zod/try=> ;;(tape [50 51 52])
    ! exit
