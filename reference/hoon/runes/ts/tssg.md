#[tissig, `=~`, %tssg](#tssg)

[Short description]

#Syntax

`=~`, `tissig`, `[%tssg p=tusk]` is a synthetic hoon that
composes a list of twigs.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

=~    i.p
        i.t.p
        i.t.t.p
    ==
 
Queenside:

    =~  i.p
        i.t.p
        i.t.t.p
    ==

##Wide form

None

##Irregular form

None

##Examples

    ~zod/try=> =~(~ [1 2 3 .] [+ +])
    [[2 3 ~] 2 3 ~]
    ~zod/try=> =~  ~
                   |%
                   ++  ham  1
                   ++  tel  2
                   --
                   |.(ham)
               ==
    <1.epy 2.msr %~>
