#[centis, `%=`, %cnts](#cnts)

[Short description]

#Syntax

`%=`, `centis`, `[%cnts p=wing q=tram]` is a natural hoon that
evaluates `p` with the changes specified in `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

%=  p
      p.i.q    q.i.q
      p.i.t.q  q.i.t.q
    ==

##Wide form

%=(p p.i.q q.i.q, p.i.t.q q.i.t.q)

##Irregular form

p(p.i.q q.i.q, p.i.t.q q.i.t.q)

##Examples



