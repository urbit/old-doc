#bucwut `$?` %bcwt

[Short description]

#Syntax

`$?`, `bucwut`, is a tile hoon that produces a `%fern`:

    [%fern p=[i=tile t=(list tile)]]

A non-empty list of cases; its icon is naturally a `%fork`. The programmer is
responsible for ensuring that the cases are actually orthogonal (unlike with
the structured forks, `%bush`, `%kelp` and `%reed`). A good general practice
is to use ferns only with leaves.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

$?  p
        q
    ==

##Wide form

None

##Irregular form

?(p q)

##Examples

++  base  ?([%atom p=odor] %noun %cell %bean %null)     ::  axils, @ * ^ ? ~

In ++base, `?` (the irregular form of $?) specifies a list of orthoganal casesfor the %axil tile.

