#[bartis, `|=`, %brts](#brts)

[Short description]

#Syntax

`|=`, `bartis`, `[%brts p=tile q=twig]` is a synthetic hoon that
produces a dry `%gold` gate with arm `q`, sample `[%bctr p]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|=  p
    q

##Wide form

|=(p q)

##Irregular form

None

##Examples

++  add                                                 ::  add
      ~/  %add
      |=  [a=@ b=@]
      ^-  @
      ?:  =(0 a)
        b
      $(a (dec a), b +(b))

In ++add, `|=` creates a gate whose sample takes two atoms
labeled `a` and `b`, and whose arm evaluates an expression that
produces the sum of the atoms.

