#bucbar `$|` %bcbr

Either atom or cell

`$|` is a tile rune that takes `++tile` `p` and `q` and produces a `%reed`,  

    [%reed p=tile q=tile]

a tile whose [icon]() contains two kinds of nouns: [atoms]() of `tile` `p` and cells of `tile` `q`.

OR

`$|` is a tile rune that takes `++tile` `p` and `q` and produces a `[%reed p=tile q=tile]` a tile whose [icon]() contains two kinds of nouns: [atoms]() of `tile` `p` and cells of `tile` `q`.

##Produces

[`Tile`]()

##Sample

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

