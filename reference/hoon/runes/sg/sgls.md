#[siglus, `~+`, %sgls](#sgls)

[Short description]

#Syntax

`~+`, `siglus`, `[%sgls p=twig]` is a synthetic hoon that
hints to the interpreter to memoize (cache) the computation 
of `p`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

~+  p

##Wide form

~+(p)

##Irregular form

None

##Examples

    ~zod/try=> 20
    20
    ~zod/try=> ~+(20)
    20
    ~zod/try=> 20
    ~zod/try=> (make '20')
    [%1 p=20]
    ~zod/try=> (make '~+(20)')
    [%10 p=[p=1.869.440.365 q=[%1 p=0]] q=[%1 p=20]]
    ~zod/try=> `@tas`1.869.440.365
    %memo
