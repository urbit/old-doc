section 2eJ, formatting (basic text)  

###++cass

```
++  cass                                                ::  lowercase
  |=  vib=tape
  %+  rap  3
  (turn vib |=(a=@ ?.(&((gte a 'A') (lte a 'Z')) a (add 32 a))))
::
```

Produce the case insensitive (all lowercase) cord of a tape.

####Examples

       ~zod/try=> (cass "john doe")
        7.309.170.810.699.673.450
        ~zod/try=> `cord`(cass "john doe")
        'john doe'
        ~zod/try=> (cass "abc, 123, !@#")
        2.792.832.775.110.938.439.066.079.945.313
        ~zod/try=> `cord`(cass "abc, 123, !@#")
        'abc, 123, !@#' 

###++cuss

```
++  cuss                                                ::  uppercase
  |=  vib=tape
  ^-  @t
  %+  rap  3
  (turn vib |=(a=@ ?.(&((gte a 'a') (lte a 'z')) a (sub a 32))))
::
```

Turn all occurances of lowercase letters in any tape into uppercase letters, as a cord.

####Examples

        ~zod/try=> (cuss "john doe")
        'JOHN DOE'
        ~zod/try=> (cuss "abc ABC 123 !@#")
        'ABC ABC 123 !@#'
        ~zod/try=> `@ud`(cuss "abc")
        4.407.873
        ~zod/try=> (cuss "AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsQqRrVvWwXxYyZz")
        'AABBCCDDEEFFGGHHIIJJKKLLMMNNOOPPQQRRSSQQRRVVWWXXYYZZ'

###++crip

```
++  crip  |=(a=tape `@t`(rap 3 a))                      ::  tape to cord
::
```

Produce the cord of a tape.

####Examples

        ~zod/try=> (crip "john doe")
        'john doe'
        ~zod/try=> (crip "abc 123 !@#")
        'abc 123 !@#'
        ~zod/try=> `@ud`(crip "abc")
        6.513.249

###++mesc

```
++  mesc                                                ::  ctrl code escape
  |=  vib=tape
  ^-  tape
  ?~  vib
    ~
  ?:  =('\\' i.vib)
    ['\\' '\\' $(vib t.vib)]
  ?:  ?|((gth i.vib 126) (lth i.vib 32) =(39 i.vib))
    ['\\' (weld ~(rux at i.vib) (runt [1 47] $(vib t.vib)))]
  [i.vib $(vib t.vib)]
::
```

###++runt

###++sand

```
++  sand                                                ::  atom sanity
  |=  a=@ta
  |=  b=@  ^-  (unit ,@)
  ?.(((sane a) b) ~ [~ b])
::
```

###++sane

###++trim

```
++  trim                                                ::  tape split
  |=  [a=@ b=tape]
  ^-  [p=tape q=tape]
  ?~  b
    [~ ~]
  ?:  =(0 a)
    [~ b]
  =+  c=$(a (dec a), b t.b)
  [[i.b p.c] q.c]
::
```

###++trip

###++teff

```
++  teff                                                ::  length utf8
  |=  a=@t  ^-  @
  =+  b=(end 3 1 a)
  ?:  =(0 b)
    ?>(=(0 a) 0)
  ?>  |((gte b 32) =(10 b))
  ?:((lte b 127) 1 ?:((lte b 223) 2 ?:((lte b 239) 3 4)))
::
```

###++turf

###++tuba

```
++  tuba                                                ::  utf8 to utf32 tape
  |=  a=tape
  ^-  (list ,@c)
  (rip 5 (turf (rap 3 a)))                              ::  XX horrible
::
```

###++tufa

###++tuft

```
++  tuft                                                ::  utf32 to utf8 text
  |=  a=@c
  ^-  @t
  %+  rap  3
  |-  ^-  (list ,@)
  ?:  =(0 a)
    ~
  =+  b=(end 5 1 a)
  =+  c=$(a (rsh 5 1 a))
  ?:  (lth b 0x7f)
    [b c]
  ?:  (lth b 0x7ff)
    :*  (mix 0b1100.0000 (cut 0 [6 5] b))
        (mix 0b1000.0000 (end 0 6 b))
        c
    ==
  ?:  (lth b 0xffff)
    :*  (mix 0b1110.0000 (cut 0 [12 4] b))
        (mix 0b1000.0000 (cut 0 [6 6] b))
        (mix 0b1000.0000 (end 0 6 b))
        c
    ==
  :*  (mix 0b1111.0000 (cut 0 [18 3] b))
      (mix 0b1000.0000 (cut 0 [12 6] b))
      (mix 0b1000.0000 (cut 0 [6 6] b))
      (mix 0b1000.0000 (end 0 6 b))
      c
  ==
::
```

###++wack

###++wick

```
++  wick                                                ::  span format
  |=  a=@
  ^-  @ta
  =+  b=(rip 3 a)
  %+  rap  3
  |-  ^-  tape
  ?~  b
    ~
  ?:  =('~' i.b)
    ?~  t.b  !!
    [?:(=('~' i.t.b) '~' ?>(=('-' i.t.b) '_')) $(b t.t.b)]
  [i.b $(b t.b)]
::
```

###++woad

###++wood

```
++  wood                                                ::  span format
  |=  a=@t
  ^-  @ta
  %+  rap  3
  |-  ^-  (list ,@)
  ?:  =(0 a)
    ~
  =+  b=(teff a)
  =+  c=(turf (end 3 b a))
  =+  d=$(a (rsh 3 b a))
  ?:  ?|  &((gte c 'a') (lte c 'z'))
          &((gte c '0') (lte c '9'))
          =('-' c)
      ==
    [c d]
  ?+  c
    :-  '~'
    =+  e=(met 2 c)
    |-  ^-  tape
    ?:  =(0 c)
      ['.' d]
    =.  e  (dec e)
    =+  f=(rsh 2 e c)
    [(add ?:((lte f 9) 48 87) f) $(c (end 2 e c))]
  ::
    %' '  ['.' d]
    %'.'  ['~' '.' d]
    %'~'  ['~' '~' d]
  ==
```


