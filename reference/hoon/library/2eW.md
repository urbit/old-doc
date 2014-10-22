##section 2eW, lite number theory           
---

###++egcd

```
++  egcd                                                ::  schneier's egcd
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


XX document

###++pram

```
++  pram                                                ::  rabin-miller
  |=  a=@  ^-  ?
  ?:  ?|  =(0 (end 0 1 a))
          =(1 a)
          =+  b=1
          |-  ^-  ?
          ?:  =(512 b)
            |
          ?|(=+(c=+((mul 2 b)) &(!=(a c) =(a (mul c (div a c))))) $(b +(b)))
      ==
    |
  =+  ^=  b
      =+  [s=(dec a) t=0]
      |-  ^-  [s=@ t=@]
      ?:  =(0 (end 0 1 s))
        $(s (rsh 0 1 s), t +(t))
      [s t]
  ?>  =((mul s.b (bex t.b)) (dec a))
  =+  c=0
  |-  ^-  ?
  ?:  =(c 64)
    &
  =+  d=(~(raw og (add c a)) (met 0 a))
  =+  e=(~(exp fo a) s.b d)
  ?&  ?|  =(1 e)
          =+  f=0
          |-  ^-  ?
          ?:  =(e (dec a))
            &
          ?:  =(f (dec t.b))
            |
          $(e (~(pro fo a) e e), f +(f))
      ==
      $(c +(c))
  ==
::
```


XX document

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


XX document

###++fo

```
++  fo                                                  ::  modulo prime
  |_  a=@
```

XX DO NOT RERUN GET.LS, THERE EXIST ARM COLLISIONS

XX document

###++dif

```
  ++  dif
    |=  [b=@ c=@]
    (sit (sub (add a b) (sit c)))
  ::
```

XX document

###++exp

```
  ++  exp
    |=  [b=@ c=@]
    ?:  =(0 b)
      1
    =+  d=$(b (rsh 0 1 b))
    =+  e=(pro d d)
    ?:(=(0 (end 0 1 b)) e (pro c e))
  ::
```

XX document

###++fra

```
  ++  fra
    |=  [b=@ c=@]
    (pro b (inv c))
  ::
```

XX document

###++inv

```
  ++  inv
    |=  b=@
    =+  c=(dul:si u:(egcd b a) a)
    c
  ::
```

XX document

###++pro

```
  ++  pro
    |=  [b=@ c=@]
    (sit (mul b c))
  ::
```

XX document

###++sit

```
  ++  sit
    |=  b=@
    (mod b a)
  ::
```

XX document

###++sum

```
  ++  sum
    |=  [b=@ c=@]
    (sit (add b c))
  --
```

XX document

###++ga

```
++  ga                                                  ::  GF (bex p.a)
  |=  a=[p=@ q=@ r=@]                                   ::  dim poly gen
  =+  si=(bex p.a)
  =+  ma=(dec si)
  =>  |%
```

XX document


###++dif

```
      ++  dif                                           ::  add and sub
        |=  [b=@ c=@]
        ~|  [%dif-ga a]
        ?>  &((lth b si) (lth c si))
        (mix b c)
      ::
```

XX document

###++dub

```
      ++  dub                                           ::  mul by x
        |=  b=@
        ~|  [%dub-ga a]
        ?>  (lth b si)
        ?:  =(1 (cut 0 [(dec p.a) 1] b))
          (dif (sit q.a) (sit (lsh 0 1 b)))
        (lsh 0 1 b)
      ::
```

XX document

###++pro

```
      ++  pro                                           ::  slow multiply
        |=  [b=@ c=@]
        ?:  =(0 b)
          0
        ?:  =(1 (dis 1 b))
          (dif c $(b (rsh 0 1 b), c (dub c)))
        $(b (rsh 0 1 b), c (dub c))
      ::
```

XX document

###++toe

```
      ++  toe                                           ::  exp/log tables
        =+  ^=  nu
            |=  [b=@ c=@]
            ^-  (map ,@ ,@)
            =+  d=*(map ,@ ,@)
            |-
            ?:  =(0 c)
              d
            %=  $
              c  (dec c)
              d  (~(put by d) c b)
            ==
        =+  [p=(nu 0 (bex p.a)) q=(nu ma ma)]
        =+  [b=1 c=0]
        |-  ^-  [p=(map ,@ ,@) q=(map ,@ ,@)]
        ?:  =(ma c)
          [(~(put by p) c b) q]
        %=  $
          b  (pro r.a b)
          c  +(c)
          p  (~(put by p) c b)
          q  (~(put by q) b c)
        ==
      ::
```

XX document

###++sit

```
      ++  sit                                           ::  reduce
        |=  b=@
        (mod b (bex p.a))
      --
```

XX document

###++fra

```
  ++  fra                                               ::  divide
    |=  [b=@ c=@]
    (pro b (inv c))
  ::
```

XX document

###++inv

```
  ++  inv                                               ::  invert
    |=  b=@
    ~|  [%inv-ga a]
    =+  c=(~(get by q) b)
    ?~  c  !!
    =+  d=(~(get by p) (sub ma u.c))
    (need d)
  ::
```

XX document

###++pow

```
  ++  pow                                               ::  exponent
    |=  [b=@ c=@]
    =+  [d=1 e=c f=0]
    |-
    ?:  =(p.a f)
      d
    ?:  =(1 (cut 0 [f 1] b))
      $(d (pro d e), e (pro e e), f +(f))
    $(e (pro e e), f +(f))
  ::
```

XX document

###++pro

```
  ++  pro                                               ::  multiply
    |=  [b=@ c=@]
    ~|  [%pro-ga a]
    =+  d=(~(get by q) b)
    ?~  d  0
    =+  e=(~(get by q) c)
    ?~  e  0
    =+  f=(~(get by p) (mod (add u.d u.e) ma))
    (need f)
  --
```

XX document

---
