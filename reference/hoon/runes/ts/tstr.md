#[tistar, `=*`, %tstr](#tstr)

[Short description]

#Syntax

`=*`, `tistar`, `[%tstr p=term q=wing r=twig]` is a natural hoon
that creates a `%bull`, or alias, type.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

=*  p  q
        r

##Wide form

=*(p q r)

##Irregular form

None

##Examples

    ~zod/try=> =+  a=[b=1 c=2]
               =*  d  b.a
               [d 3]
    [1 3]
