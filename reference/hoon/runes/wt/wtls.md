#[wutlus, `?+`, %wtls](#wtls)

[Short description]

#Syntax

`?+`, `wutlus`, `[%wtls p=wing q=twig r=tine]` is a synthetic
hoon that selects a case in `q` for the actual type of `p`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

Kingside:

    ?+  p
      q
      p.i.r      q.i.r
      p.i.t.r    q.i.t.r
      p.i.t.t.r  q.i.t.t.r
    ==

Queenside:

    ?+    p
      q
        p.i.r      
      q.i.r
        p.i.t.r    
      q.i.t.r
        p.i.t.t.r  
      q.i.t.t.r
    ==

##Wide form

?+(p p.i.r q.i.r, p.i.t.r q.i.t.r, p.i.t.t.r q.i.t.t.r)

##Irregular form

None

##Examples


    ~zod/try=> ?+  'b'  ~
                 %a  [~ 5]
                 %b  [~ 7]
                 %c  [~ 3]
               ==
    [~ 7]
    ~zod/try=> ?+  'd'  ~
                 %a  [~ 5]
                 %b  [~ 7]
                 %c  [~ 3]
               ==
    ~
