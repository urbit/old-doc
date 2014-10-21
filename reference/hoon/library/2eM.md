##section 2eM, regular-expressions      

###++pars

```
++  pars
  |=  [a=tape]                                          ::  parse tape to rege
  ^-  (unit rege)
  =+  foo=((full anns) [[1 1] a])
  ?~  q.foo
    ~
  [~ p.u.q.foo]
::
```

###++nor

###++les  

```
++  les  ;~(pose (shim 32 91) (shim 93 126))
```
###++lep  

###++alm  

```
++  alm  (shim 32 126)
```

###++alb  

###++mis  

```
++  mis  ;~(pose (shim 32 47) (shim 58 64) (shim 91 96) (shim 123 126))
::
```

###++anns 

###++mall

```
++  mall
  %+  knee  *rege  |.  ~+
  ;~((bend |=(a=[rege rege] (some [%pair a]))) bets mall)
::
```

###++bets

###++ranc

```
++  ranc
  |=  [a=@ b=@]
  ^-  @
  ?:((gth a b) 0 (con (bex a) $(a +(a))))
::
```

###++flap 

###++rang

```
++  rang
  %+  sear  |=([a=@ b=@] ?:((lte a b) (some [a b]) ~))
    (ifix [kel ker] ;~(plug dim:ag ;~(pfix com dim:ag)))
::
```

###++chun

###++seac

```
++  seac
  |=  tub=nail
  ?~  q.tub
    (fail tub)
  ?:  =(i.q.tub '^')
    (;~(pfix ket (cook flap sead)) tub)
  (sead tub)
::
```

###++sead

###++sade

```
++  sade
  %+  knee  *@  |.  ~+
  ;~  pose
    (cold (bex '-') (jest '-]'))
    (cold 0 ser)
    (cook |=([p=@ q=@] `@`(con p q)) ;~(plug seap sade))
  ==
::
```

###++seap

###++cape

```
++  cape
  %+  knee  *tape  |.  ~+
  ;~  pose
    (cold ~ (jest '\\E'))
    ;~(plug next cape)
    (cook |=(a=char (tape [a ~])) next)
    (full (easy ~))
  ==
::
```

###++lower

###++upper

```
++  upper  (ranc 'A' 'Z')
```

###++digit

###++print

```
++  print  (ranc 32 126)
```

###++graph

###++blank

```
++  blank  (con (bex 32) (bex 9))
```

###++space

###++cntrl

```
++  cntrl  :(con (ranc 0 31) (bex 127))
```

###++alpha

###++alnum

```
++  alnum  :(con lower upper digit)
```

###++punct

###++wordc

```
++  wordc  :(con digit lower upper (bex 95))
```

###++white

###++xdigit

``````

###++chad

###++escd

```
++  escd
  %+  knee  *@  |.  ~+
  ;~  pose
    (cold (bex 7) (just 'a'))
    (cold (bex 9) (just 't'))
    (cold (bex 10) (just 'n'))
    (cold (bex 11) (just 'v'))
    (cold (bex 12) (just 'f'))
    (cold (bex 13) (just 'r'))
    (cold (bex 0) (just '0'))
    (sear |=(a=@ ?:((lth a 256) (some (bex a)) ~)) (bass 8 (stun [2 3] cit)))
    (cook bex ;~(pfix (just 'x') (bass 16 (stun [2 2] hit))))
    (cook bex (ifix [(jest 'x{') ker] (bass 16 (stun [2 2] hit))))
    (cook bex mis)
  ==
::
```

###++escp

###++unid

```
++  unid
  %+  knee  *@  |.  ~+
  ;~  pose
    (cold digit (jest '\\d'))
    (cold (flap digit) (jest '\\D'))
    (cold white (jest '\\s'))
    (cold (flap white) (jest '\\S'))
    (cold wordc (jest '\\w'))
    (cold (flap wordc) (jest '\\W'))
  ==
::
```

###++proc 

###++cont

```
++  cont
  |=  [a=(map ,@u tape) b=(map ,@u tape)]
  (~(gas by _(map ,@u tape)) (weld (~(tap by a)) (~(tap by b))))
::
```

###++abor

###++matc

```
++  matc
  |=  [a=rege b=tape c=tape]
  ^-  (unit (map ,@u tape))
  =+  foo=`(unit ,[tape (map ,@u tape)])`(deep a b %empt c)
  (bind foo |*(a=^ (~(put by +.a) 0 -.a)))
::
```

###++chet

###++blak 

```
++  blak  (some ["" _(map ,@u tape)])
```

###++deep

###++rexp

```
++  rexp                                                :: Regex match
  ~/  %rexp
  |=  [a=tape b=tape]
  ^-  (unit (unit (map ,@u tape)))
  =+  ^=  bar
      |=  [a=@ b=(map ,@u tape)]
      ?:  =(a 0)
        b
      =+  c=(~(get by b) a)
      ?~  c
        $(a (dec a), b (~(put by b) a ""))
      $(a (dec a))
  =+  par=(pars a)
  ?~  par  ~
  =+  poc=(proc u.par 1)
  =+  c=b
  |-
  =+  foo=(matc +.poc c b)
  ?~  foo
    ?~  c
      [~ ~]
    $(c t.c)
  [~ [~ (bar (dec -.poc) u.foo)]]
::
```
 
###++repg 
