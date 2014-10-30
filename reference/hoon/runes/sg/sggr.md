#[siggar, `~>`, %sggr](#sggr)

[Short description]

#Syntax

`~>`, `siggar`, `[%sggr p=$|(term [p=term q=twig]) q=twig]` is a
natural hoon that applies arbitrary hint `p` to `q`.
`q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

`p=%foo`:
  
    ~>  %foo
        q

    `p=[p=%foo q=bar]`:

        ~>  %foo.bar
        q

##Wide form

~>(%foo q)
    ~>(%foo.bar q)

##Irregular form

None

##Examples

    ~zod/try=> (make '~>(%a 42)')
    [%10 p=97 q=[%1 p=42]]
    ~zod/try=> (make '~>(%a.+(2) 42)')
    [%10 p=[p=97 q=[%4 p=[%1 p=2]]] q=[%1 p=42]]
