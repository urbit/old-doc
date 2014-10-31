#[zapsem, `!;`, %zpsm](#zpsm)

[Short description]

#Syntax

`!;`, `zapsem`, `[%zpsm p=twig q=twig]` is a natural hoon that
produces the product of twig `q` as a `[type noun]` pair, with
twig `p` serving as an example the type of the type.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

!;  p
        q

##Wide form

!;(p q)

##Irregular form

None

##Examples


    ~zod/try=> !;(*type 1)
    [[%atom p=%ud] 1]
    ~zod/try=> !;(*type [1 2])
    [[%cell p=[%atom p=%ud] q=[%atom p=%ud]] 1 2]
    ~zod/try=> !;([%atom ''] ~doznec)
    [[%atom 'p'] ~doznec]
