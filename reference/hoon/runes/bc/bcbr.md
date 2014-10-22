#bucbar `$|` %bcbr

[Short description]

#Syntax

`$|`, `bucbar`, is a tile rune that takes `++tile` `p` and `q` and produces a `%reed`,  

    [%reed p=tile q=tile]

a `%reed` is a tile whose icon contains two kinds of nouns: atoms of tile `p` and cells of tile `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

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

In ++list, $| specifies that every element in a noun that can be cast to a ++list is either the atom ~ or the cell [i=a t=(list a)].

