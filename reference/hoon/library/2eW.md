##section 2eW, lite number theory           
---

###++egcd   

```
++  egcd  !:                                            ::  schneier's egcd
  |=  [a=@ b=@]
  =+  si
  =+  [c=(sun a) d=(sun b)]
  =+  [u=[c=(sun 1) d=--0] v=[c=--0 d=(sun 1)]]
  |-  ^-  [d=@ u=@ v=@]
  ?:  =(--0 c)
    [(abs d) d.u d.v]
  ::  ?>  ?&  =(c (sum (pro (sun a) c.u) (pro (sun b) c.v)))
  ::          =(d (sum (pro (sun a) d.u) (pro (sun b) d.v)))
  ::      ==
  =+  q=(fra d c)
  %=  $
    c  (dif d (pro q c))
    d  c
    u  [(dif d.u (pro q c.u)) c.u]
    v  [(dif d.v (pro q c.v)) c.v]
  ==
::
```
###++pram   
###++ramp   

```
++  ramp                                                ::  make r-m prime
  |=  [a=@ b=(list ,@) c=@]  ^-  @ux                    ::  [bits snags seed]
  =>  .(c (shas %ramp c))
  =+  d=_@
  |-
  ?:  =((mul 100 a) d)
    ~|(%ar-ramp !!)
  =+  e=(~(raw og c) a)
  ?:  &(|-(?~(b & &(!=(1 (mod e i.b)) $(b +.b)))) (pram e))
    e
  $(c +(c), d (shax d))
::
```
###++fo     
##  ++  dif
##  ++  exp
##  ++  fra
##  ++  inv
##  ++  pro
##  ++  sit
##  ++  sum
###++ga     

```
++  ga                                                  ::  GF (bex p.a)
  |=  a=[p=@ q=@ r=@]                                   ::  dim poly gen
  =+  si=(bex p.a)
  =+  ma=(dec si)
  =>  |%
```
##      ++  dif 
##      ++  dub 
##      ++  pro 
##      ++  toe 
##      ++  sit 
##  ++  fra     
##  ++  inv     
##  ++  pow     
##  ++  pro     

---

