#[sigcab, `~_`, %sgcb](#sgcb)

[Short description]

#Syntax

`~_`, `sigcab`, `[%sgcb p=twig q=twig]` is a synthetic hoon
that inserts `p`, a trap producing `tank`, in the trace of `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

~_  p
        q

##Wide form

~_(p q)

##Irregular form

None

##Examples

    ~zod/try=> (make '~_(+216 ~)')
    [%10 p=[p=1.851.876.717 q=[p=[%1 p=[0 216]] q=[%0 p=1]]] q=[%1 p=0]]
    ~zod/try=> `@tas`1.851.876.717
    %mean
