#bucbar `$|` %bcbr

Fork of either atom or cell

`$|` is a tile rune that produces a , a tile whose [icon]() is a [fork]() between two kinds of nouns: [atoms]() of `tile` `p` and cells of `tile` `q`. `$|` is a fork tile similar to [`$?`](), but is more strict in that in only contains one atom tile and one cell tile.

##Produces

[`Tile`](): `[%reed p=tile q=tile]`

`p` is a [`tile`]()
`q` is a [`tile`]() 

##Tall form

$|  p
        q
    ==

##Wide form

$|(p q)

##Irregular form

None

##Examples

++  list  |*  a=_,*                                     ::  null-terminated list
              $|(~ [i=a t=(list a)])                        ::

In ++list, `$|` specifies that every element in a noun that can be cast to a ++list is either the atom ~ or the cell [i=a t=(list a)].

