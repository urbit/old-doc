#[semcol, `;:`, %smcl](#smcl)

[Short description]

#Syntax

`;:`, `semcol`, `[%smcl p=twig q=tusk]` is a synthetic hoon that
applies `p`, a binary gate, to the n-ary tuple `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

;:  p
      i.q
      i.t.q
      i.t.t.q
    ==

##Wide form

;:(p i.q i.t.q i.t.t.q)

##Irregular form

:(p i.q i.t.q i.t.t.q)

##Examples



