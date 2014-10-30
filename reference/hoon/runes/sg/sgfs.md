#[sigfas, `~/`, %sgfs](#sgfs)

[Short description]

#Syntax

`~/`, `sigfas`, `[%sgfs p=term q=twig]` is a synthetic hoon that
implements one common case - a gate arm in a book, ie, a library
function - of the `%sgcn` jet hint.  `%sgfs` assumes the parent
axis is `7` and there are no children.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

~/  p
        q

##Wide form

~/(p q)

##Irregular form

None

##Examples

    ~zod/try=> (make '~/  %bam  |.(40)')
    [%8 p=[%1 p=[1 40]] q=[%10 p=[p=1.953.718.630 q=[%1 p=[7.168.354 [0 7] 0]]] q=[%0 p=1]]]
    ~zod/try=> `@`%bam
    7.168.354
    ~zod/try=> `@tas`1.953.718.630
    %fast
