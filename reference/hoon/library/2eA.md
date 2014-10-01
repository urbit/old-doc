section 2eA, packing          

---

###++cue

```
++  cue                                                 ::  unpack
  ~/  %cue
  |=  a=@
  ^-  *
  =+  b=0
  =+  m=`(map ,@ ,*)`~
  =<  q
  |-  ^-  [p=@ q=* r=_m]
  ?:  =(0 (cut 0 [b 1] a))
    =+  c=(rub +(b) a)
    [+(p.c) q.c (~(put by m) b q.c)]
  =+  c=(add 2 b)
  ?:  =(0 (cut 0 [+(b) 1] a))
    =+  u=$(b c)
    =+  v=$(b (add p.u c), m r.u)
    =+  w=[q.u q.v]
    [(add 2 (add p.u p.v)) w (~(put by r.v) b w)]
  =+  d=(rub c a)
  [(add 2 p.d) (need (~(get by m) q.d)) m]
::
```

Unpack an atom to a noun.  The inverse of jam.

####Examples        
 
        ~midlys-rocpet/try=> (cue (jam 1))
        1
        ~midlys-rocpet/try=> (cue 4.657)
        [1 2]
        ~midlys-rocpet/try=> (cue (jam [1 1]))
        [1 1]
        ~tadbyl-hilbel/try=> (cue 39.689)
        [0 19]

---

###++jam       

```
++  jam                                                 ::  pack
  ~/  %jam
  |=  a=*
  ^-  @
  =+  b=0
  =+  m=`(map ,* ,@)`~
  =<  q
  |-  ^-  [p=@ q=@ r=_m]
  =+  c=(~(get by m) a)
  ?~  c
    =>  .(m (~(put by m) a b))
    ?:  ?=(@ a)
      =+  d=(mat a)
      [(add 1 p.d) (lsh 0 1 q.d) m]
    =>  .(b (add 2 b))
    =+  d=$(a -.a)
    =+  e=$(a +.a, b (add b p.d), m r.d)
    [(add 2 (add p.d p.e)) (mix 1 (lsh 0 2 (cat 0 q.d q.e))) r.e]
  ?:  ?&(?=(@ a) (lte (met 0 a) (met 0 u.c)))
    =+  d=(mat a)
    [(add 1 p.d) (lsh 0 1 q.d) m]
  =+  d=(mat u.c)
  [(add 2 p.d) (mix 3 (lsh 0 2 q.d)) m]
::
```

Compress a noun to an atom.  The inverse of cue.

####Examples

        ~midlys-rocpet/try=> (jam 1)
        12
        ~midlys-rocpet/try=> (jam [1 1])
        817
        ~tadbyl-hilbel/try=> (jam [~ u=19])
        39.689

---

###++mat       

```
++  mat                                                 ::  length-encode
  ~/  %mat
  |=  a=@
  ^-  [p=@ q=@]
  ?:  =(0 a)
    [1 1]
  =+  b=(met 0 a)
  =+  c=(met 0 b)
  :-  (add (add c c) b)
  (cat 0 (bex c) (mix (end 0 (dec c) b) (lsh 0 (dec c) a)))
::
```

Encodes length.  Only used internally as helper function to jam and cue.

####Examples

---

###++rub 

```
++  rub                                                 ::  length-decode
  ~/  %rub
  |=  [a=@ b=@]
  ^-  [p=@ q=@]
  =+  ^=  c
      =+  [c=0 m=(met 0 b)]
      |-  ?<  (gth c m)
      ?.  =(0 (cut 0 [(add a c) 1] b))
        c
      $(c +(c))
  ?:  =(0 c)
    [1 0]
  =+  d=(add a +(c))
  =+  e=(add (bex (dec c)) (cut 0 [d (dec c)] b))
  [(add (add c c) e) (cut 0 [(add d (dec c)) e] b)]
```

Decodes length.  Only used internally as a helper function to jam and cue.

####Examples

---


