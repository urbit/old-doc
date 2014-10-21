#[barket, `|^`, %brkt](#brkt)

[Short description]

#Syntax

`|^`, `barket`, `[%brkt p=twig q=(map term foot)]` is a synthetic hoon
that produces a `%gold` book with arms `q`, plus `p` as `%$`, and 
kicks it.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|^  p
      ++  p.n.q
        q.n.q
    --

##Wide form

None

##Irregular form

None

##Examples

In ++mint, |^ creates a book whose `$` arm compiles twigs to Nock, and whose other arms contain useful expressions for that compilation.

