#buccen `$%` %bccn

[Short description]

#Syntax

`$%`, `buccen`, is a tile hoon that produces a %kelp. `$%` takes a list of lines, which are labeleed cases, closed by `==`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

$%  p
        q
        q
    ==

##Wide form

None

##Irregular form

None

##Examples

++  foot  $%  [%ash p=twig]                             ::  dry, geometric
                  [%elm p=twig]                             ::  wet, generic
                  [%oak ~]                                  ::  XX not used
                  [%yew p=(map term foot)]                  ::  XX not used
              ==

In ++foot, `$%` creates a %kelp, which is a list of possible cases. That is, a ++foot can be either %ash, %elm, %oak or %yew.

