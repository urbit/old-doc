#[cendot, `%.`, %cndt](#cndt)

[Short description]

#Syntax

`%.`, `cendot`, `[%cndt p=twig q=twig]` is a synthetic hoon that
reverses the order of `%cnhp`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

%.  p
    q

##Wide form

%.(p q)

##Irregular form

None

##Examples

~waclux-tomwyc/try=> %.(42 dec)
    41

In the above example, `%.` slams ++dec with the sample 42.

