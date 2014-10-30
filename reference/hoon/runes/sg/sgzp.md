#[sigzap, `~!`, %sgzp](#sgzp)

[Short description]

#Syntax

`~!`, `sigzap`, `[%sgzp p=twig q=twig]` is a natural hoon for 
debugging uses only, semantically equivalent to its own twig `q`.
But if compilation fails within `q`, `~!` will show the type of
`p` on the stacktrace.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

~!  p
        q

##Wide form

~!(p q)

##Irregular form

None

##Examples

    ~zod/try=> a
    ! -find-limb.a
    ! find-none
    ! exit
    ~zod/try=> ~!('foo' a)
    ! @t
    ! -find-limb.a
    ! find-none
    ! exit
    ~zod/try=> ~!(%foo a)
    ! %foo
    ! -find-limb.a
    ! find-none
    ! exit
    ~zod/try=> ~!(*(list ,@) a)
    ! it(@)
    ! -find-limb.a
    ! find-none
    ! exit
