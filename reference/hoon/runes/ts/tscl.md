#[tiscol, `=:`, %tscl](#tscl)

[Short description]

#Syntax

`=:`, `tiscol`, `[%tscl p=tram q=twig]` is a synthetic hoon that produces `q` with the subject modified by `p`.

See also `=.`

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

=:  p.i.p      q.i.p
        p.i.t.p    q.i.t.p
        p.i.t.t.p  q.i.t.t.p
      ==
    q

##Wide form

None

##Irregular form

None

##Examples

    ~zod/try=> =+  a=[b=1 c=2]
               =:  c.a  4
                   b.a  3
                 ==
               a
    [b=3 c=4]
