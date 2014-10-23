#buccen `$%` %bccn

Tagged union

#Syntax

`$%`, `buccen`, is a tile rune that produces a (), the tile of the discriminated union. `$%` takes a list of lines, which are labeled cases, called fronds closed by `==`. Commonly usesd for pattern matching.

##Produces

[Twig](): [`[%kelp p=[i=line t=(list line)]`]]

`p` is a [list]() of [line]().

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

