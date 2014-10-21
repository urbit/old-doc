#[siggal, `~<`, %sggl](#sggl)

[Short description]

#Syntax

`~<`, `siggal`, `[%sggl p=$|(term [p=term q=twig]) q=twig]` is a
synthetic hoon that applies arbitrary hint `p` to the product of 
`q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

`p=%foo`:
      
        ~<  %foo
        q

    `p=[p=%foo q=bar]`:

        ~<  %foo.bar
        q

##Wide form

~<(%foo q)
    ~<(%foo.bar q)

##Irregular form

None

##Examples



