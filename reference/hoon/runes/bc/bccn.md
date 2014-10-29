#[buccen `$%` %bccn](#bccn)

Tagged union

`$%` is a tile rune that produces a [`%kelp`](), the tile of the discriminated union. `$%` takes a list of lines which are labeled cases, called fronds, closed by `==`. Commonly used for pattern matching.

##Produces

[Twig](): `[%kelp p=[i=line t=(list line)]]`

##Sample

`p` is a [`++list`]() of [`++line`]()s.

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

In `++foot`, `$%` creates a list of possible cases. That is, a `++foot` can be either `%ash`, `%elm`, `%oak` or `%yew`.

