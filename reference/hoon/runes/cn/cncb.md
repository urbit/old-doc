#[cencab, `%_`, %cncb](#cncb)

[Short description]

#Syntax

`%_`, `cencab`, `[%cncb p=wing q=tram]` is a synthetic hoon that
evaluates `p` with the changes specified in `q`, then casts the
product back to `p`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

%_  p
      p.i.q  q.i.q
      p.i.t.q  q.i.t.q
    ==

##Wide form

%_(p p.i.q q.i.q, p.i.t.q q.i.t.q)

##Irregular form

None

##Examples



