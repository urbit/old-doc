##section 2eC, parsing (custom rules)   

###++cold  

Replace with constant

```
++  cold                                                ::  replace w/ constant
  ~/  %cold
  |*  [cus=* sef=_rule]
  ~/  %fun
  |=  tub=nail
  =+  vex=(sef tub)
  ?~  q.vex
    vex
  [p=p.vex q=[~ u=[p=cus q=q.u.q.vex]]]
::
```

Parser modifier: produces a rule that produces a constant `cus` if `sef` is successful.

`cus` is a constant [noun]().

`sef` is a [rule]().

`tub` is a [nail]().

        ~zod/try=> ((cold %foo (just 'a')) [[1 1] "abc"])
        [p=[p=1 q=2] q=[~ u=[p=%foo q=[p=[p=1 q=2] q="bc"]]]]
        ~zod/try=> ((cold %foo (just 'a')) [[1 1] "bc"])
        [p=[p=1 q=1] q=~]

---

###++cook

Apply gate

```
++  cook                                                ::  apply gate
  ~/  %cook
  |*  [poq=_,* sef=_rule]
  ~/  %fun
  |=  tub=nail
  =+  vex=(sef tub)
  ?~  q.vex
    vex
  [p=p.vex q=[~ u=[p=(poq p.u.q.vex) q=q.u.q.vex]]]
::
```

Parser modifier: produces a rule that takes the result of `sef` and slams it through `poq`.

`poq` is a [gate]().

`sef` is a [rule]().

`tub` is a [nail]().

        ~zod/try=> ((cook ,@ud (just 'a')) [[1 1] "abc"])
        [p=[p=1 q=2] q=[~ u=[p=97 q=[p=[p=1 q=2] q="bc"]]]]
        ~zod/try=> ((cook ,@tas (just 'a')) [[1 1] "abc"])
        [p=[p=1 q=2] q=[~ u=[p=%a q=[p=[p=1 q=2] q="bc"]]]]
        ~zod/try=> ((cook |=(a=@ +(a)) (just 'a')) [[1 1] "abc"])
        [p=[p=1 q=2] q=[~ u=[p=98 q=[p=[p=1 q=2] q="bc"]]]]
        ~zod/try=> ((cook |=(a=@ `@t`+(a)) (just 'a')) [[1 1] "abc"])
        [p=[p=1 q=2] q=[~ u=[p='b' q=[p=[p=1 q=2] q="bc"]]]]

---

###++easy

Always parse

```
++  easy                                                ::  always parse
  ~/  %easy
  |*  huf=*
  ~/  %fun
  |=  tub=nail
  ^-  (like ,_huf)
  [p=p.tub q=[~ u=[p=huf q=tub]]]
::
```

Parser generator: produces a [rule]() that succeeds with given noun `huf` without consuming any text.

`huf` is a [noun]().

`tub` is a [nail]().

        ~zod/try=> ((easy %foo) [[1 1] "abc"])
        [p=[p=1 q=1] q=[~ [p=%foo q=[p=[p=1 q=1] q="abc"]]]]
        ~zod/try=> ((easy %foo) [[1 1] "bc"])
        [p=[p=1 q=1] q=[~ [p=%foo q=[p=[p=1 q=1] q="bc"]]]]
        ~zod/try=> ((easy 'a') [[1 1] "bc"])
        [p=[p=1 q=1] q=[~ [p='a' q=[p=[p=1 q=1] q="bc"]]]]

---

###++fail

Never parse

```
++  fail  |=(tub=nail [p=p.tub q=~])                    ::  never parse
```

Produces an [edge]() at the same text position ([hair]()) with a failing result (`q=~`).

`tub` is a [nail]().

        ~zod/try=> (fail [[1 1] "abc"])
        [p=[p=1 q=1] q=~]
        ~zod/try=> (fail [[p=1.337 q=70] "Parse me, please?"])
        [p=[p=1.337 q=70] q=~]

---

###++full  

Parse to end

```
++  full                                                :: parse to end 
  |*  sef=_rule
  |=  tub=nail
  =+  vex=(sef tub)
  ?~(q.vex vex ?:(=(~ q.q.u.q.vex) vex [p=p.vex q=~]))
::
```

Produces a parser that succeeds only when a `sef` success consumes the remainder of the [tape](). 

`sef` is a [rule]().

`tub` is a [nail]()

        ~zod/try=> ((full (just 'a')) [[1 1] "ab"])
        [p=[p=1 q=2] q=~]
        ~zod/try=> ((full (jest 'ab')) [[1 1] "ab"])
        [p=[p=1 q=3] q=[~ u=[p='ab' q=[p=[p=1 q=3] q=""]]]]
        ~zod/try=> ((full ;~(plug (just 'a') (just 'b'))) [[1 1] "ab"])
        [p=[p=1 q=3] q=[~ u=[p=[~~a ~~b] q=[p=[p=1 q=3] q=""]]]]

---

###++funk

Prepend, parse

```
++  funk                                                ::  add to tape first
  |*  [pre=tape sef=_rule]
  |=  tub=nail
  (sef p.tub (weld pre q.tub))
::
```

Parser modifier: prepend text to tape before applying parser. Does not modify the [hair]() of `tub`.

`pre` is a [tape]().

`sef` is a [rule]().

`tub` is a [nail]().

        ~zod/try=> ((funk "abc prefix-" (jest 'abc')) [[1 1] "to be parsed"])
        [p=[p=1 q=4] q=[~ [p='abc' q=[p=[p=1 q=4] q=" prefix-to be parsed"]]]]
        ~zod/try=> ((funk "parse" (just 'a')) [[1 4] " me"])
        [p=[p=1 q=4] q=~]

---

###++here

Place-based apply

```
++  here                                                ::  place-based apply
  ~/  %here
  |*  [hez=_|=([a=pint b=*] [a b]) sef=_rule]
  ~/  %fun
  |=  tub=nail
  =+  vex=(sef tub)
  ?~  q.vex
    vex
  [p=p.vex q=[~ u=[p=(hez [p.tub p.q.u.q.vex] p.u.q.vex) q=q.u.q.vex]]]
::
```

Parser modifier: produces a [rule]() that takes a (successful) result of `sef` and slams it through `poq`, which also accepts a pint `a`. Used in parser to produce stack traces for debugging. Similar to [++cook]().

`hez` is a [gate]() that accepts a [pint]() (pair of trace locations) and the parsed result of `sef`.

`sef` is a [rule]().

`tub` is a [nail]().

    ~zod/try=> (scan "abc" (star alf))
    "abc"
    ~zod/try=> (scan "abc" (here |*(^ +<) (star alf)))
    [[[p=1 q=1] p=1 q=4] "abc"]
    ~zod/try=> (scan "abc" (star (here |*(^ +<) alf)))
    ~[[[[p=1 q=1] p=1 q=2] ~~a] [[[p=1 q=2] p=1 q=3] ~~b] [[[p=1 q=3] p=1 q=4] ~~c]]

---
        
###++inde

Enforce indendation block

```
++  inde  |*  sef=_rule                                 :: indentation block
  |=  nail  ^+  (sef)
  =+  [har tap]=[p q]:+<
  =+  lev=(fil 3 (dec q.har) ' ')
  =+  eol=(just `@t`10)
  =+  =-  roq=((star ;~(pose prn ;~(sfix eol (jest lev)) -)) har tap)
      ;~(simu ;~(plug eol eol) eol)
  ?~  q.roq  roq
  =+  vex=(sef har(q 1) p.u.q.roq)
  =+  fur=p.vex(q (add (dec q.har) q.p.vex))
  ?~  q.vex  vex(p fur)
  =-  vex(p fur, u.q -)
  :+  &3.vex
    &4.vex(q.p (add (dec q.har) q.p.&4.vex))
  =+  res=|4.vex
  |-  ?~  res  |4.roq
  ?.  =(10 -.res)  [-.res $(res +.res)]
  (welp [`@t`10 (trip lev)] $(res +.res))
::
```

Produces a [rule]() that applies `sef` to an indented block starting at the current column number, omitting the leading whitespace.

`sef` is a [rule]().

    ~zod/try=> (scan "abc" (inde (star ;~(pose prn (just `@`10)))))
    "abc"
    ~zod/try=> (scan "abc" (star ;~(pose prn (just `@`10))))
    "abc"
    ~zod/try=> (scan "  abc\0ade" ;~(pfix ace ace (star ;~(pose prn (just `@`10)))))
    "abc
        de"
    ~zod/try=> (scan "  abc\0ade" ;~(pfix ace ace (inde (star ;~(pose prn (just `@`10))))))
    ! {1 6}
    ! exit
    ~zod/try=> (scan "  abc\0a  de" ;~(pfix ace ace (inde (star ;~(pose prn (just `@`10))))))
    "abc
        de"

---

###++jest  

Match literal

```
++  jest                                                ::  match a cord
  |=  daf=@t
  |=  tub=nail
  =+  fad=daf
  |-  ^-  (like ,@t)
  ?:  =(0 daf)
    [p=p.tub q=[~ u=[p=fad q=tub]]]
  ?:  |(?=(~ q.tub) !=((end 3 1 daf) i.q.tub))
    (fail tub)
  $(p.tub (lust i.q.tub p.tub), q.tub t.q.tub, daf (rsh 3 1 daf))
::
```

Parser generator: produces a [rule]() that matches and consumes a literal `daf`. Fails if `tub` does not match `daf`.

`daf` is a [cord]().

`tub` is a [nail]().

    ~zod/try=> ((jest 'abc') [[1 1] "abc"])
    [p=[p=1 q=4] q=[~ [p='abc' q=[p=[p=1 q=4] q=""]]]]
    ~zod/try=> (scan "abc" (jest 'abc'))
    'abc'
    ~zod/try=> (scan "abc" (jest 'acb'))
    ! {1 2}
    ! 'syntax-error'
    ! exit
    ~zod/try=> ((jest 'john doe') [[1 1] "john smith"])
    [p=[p=1 q=6] q=~]
    ~zod/try=> ((jest 'john doe') [[1 1] "john doe"])
    [p=[p=1 q=9] q=[~ [p='john doe' q=[p=[p=1 q=9] q=""]]]]

---

###++just

Match char

```
++  just                                                ::  XX redundant, jest
  ~/  %just                                             ::  match a char
  |=  daf=char
  ~/  %fun
  |=  tub=nail
  ^-  (like char)
  ?~  q.tub
    (fail tub)
  ?.  =(daf i.q.tub)
    (fail tub)
  (next tub)
::
```

Produces a [rule]() that matches and consumes a single character `daf`. Fail if `tub` does not match `daf`.

`daf` is a [char]().

`tub` is an [nail]().

    ~zod/try=> ((just 'a') [[1 1] "abc"])
    [p=[p=1 q=2] q=[~ [p=~~a q=[p=[p=1 q=2] q="bc"]]]]
    ~zod/try=> (scan "abc" (just 'a'))
    ! {1 2}
    ! 'syntax-error'
    ! exit
    ~zod/try=> (scan "a" (just 'a'))
    ~~a
    ~zod/try=> (scan "%" (just '%'))
    ~~~25.

---

###++knee

Lazy parser

```
++  knee                                                ::  Lazy parser
  |*  [gar=* sef=_|.(rule)]
  |=  tub=nail
  ^-  (like ,_gar)
  ((sef) tub)
::
```

Parser modifier: produces a parser that waits until runtime to untrap and apply `sef`, which would otherwise be infinite when compiled. Used for recursive parsers.

`gar` is a [noun]().

`sef` is a [rule]().

`tub` is a [nail]().

    ~zod/try=> |-(;~(plug prn ;~(pose $ (easy ~))))
    ! rest-loop
    ! exit
    ~zod/try=> |-(;~(plug prn ;~(pose (knee *tape |.(^$)) (easy ~))))
    < 1.obo
      [ c=c=tub=[p=[p=@ud q=@ud] q=""]
          b
        < 1.bes
          [ c=tub=[p=[p=@ud q=@ud] q=""]
            b=<1.tnv [tub=[p=[p=@ud q=@ud] q=""] <1.ktu [daf=@tD <414.fvk 101.jzo 1.ypj %164>]>]>
            a=<1.fvg [tub=[p=[p=@ud q=@ud] q=""] <1.khu [[les=@ mos=@] <414.fvk 101.jzo 1.ypj %164>]>]>
            v=<414.fvk 101.jzo 1.ypj %164>
          ]
        >
          a
        ... 450 lines omitted ...
      ]
    >
    ~zod/try=> (scan "abcd" |-(;~(plug prn ;~(pose (knee *tape |.(^$)) (easy ~)))))
    [~~a "bcd"]

---

###++mask  

Match char in list

```
++  mask                                                ::  match char in set
  ~/  %mask
  |=  bud=(list char)
  ~/  %fun
  |=  tub=nail
  ^-  (like char)
  ?~  q.tub
    (fail tub)
  ?.  (lien bud |=(a=char =(i.q.tub a)))
    (fail tub)
  (next tub)
::
```

Produces a [rule]() that matches a character if it is in `bud`.

`bud` is a [list]() of chars.

    ~zod/try=> (scan "a" (mask "cba"))
    ~~a
    ~zod/try=> ((mask "abc") [[1 1] "agda"])
    [p=[p=1 q=2] q=[~ [p=~~a q=[p=[p=1 q=2] q="gda"]]]]
    ~zod/try=> ((mask "abc") [[1 1] "bgda"])
    [p=[p=1 q=2] q=[~ [p=~~b q=[p=[p=1 q=2] q="gda"]]]]
    ~zod/try=> ((mask "abc") [[1 1] "dgda"])
    [p=[p=1 q=1] q=~]

---

###++next  

Consume char

```
++  next                                                ::  consume a char
  |=  tub=nail
  ^-  (like char)
  ?~  q.tub
    (fail tub)
  =+  zac=(lust i.q.tub p.tub)
  [zac [~ i.q.tub [zac t.q.tub]]]
::
```

Consumes any character, producing an [edge]() with that character as the result.

`tub` is a [nail]().

    ~zod/try=> (next [[1 1] "ebc"])
    [p=[p=1 q=2] q=[~ [p=~~e q=[p=[p=1 q=2] q="bc"]]]] 
    ~zod/try=> (next [[1 1] "john jumps jones"])
    [p=[p=1 q=2] q=[~ [p=~~j q=[p=[p=1 q=2] q="ohn jumps jones"]]]]

---

###++sear  

Conditional cook

```
++  sear                                                ::  conditional cook
  |*  [pyq=_|=(* *(unit)) sef=_rule]
  |=  tub=nail
  =+  vex=(sef tub)
  ?~  q.vex
    vex
  =+  gey=(pyq p.u.q.vex)
  ?~  gey
    [p=p.vex q=~]
  [p=p.vex q=[~ u=[p=u.gey q=q.u.q.vex]]]
::
```

Produces a rule that slams the result of `sef` through a [gate]() that produces a [unit](); if that unit is empty, fail.

`pyq` is a [gate]() that accepts a noun and produces a [unit]().

`sef` is a [rule]().

`tub` is a [nail]().

    ~zod/try=> ((sear |=(a=* ?@(a (some a) ~)) (just `a`)) [[1 1] "abc"])
    [p=[p=1 q=2] q=[~ u=[p=97 q=[p=[p=1 q=2] q="bc"]]]]
    ~zod/try=> ((sear |=(* ~) (just 'a')) [[1 1] "abc"])
    [p=[p=1 q=2] q=~]

---

###++shim  

Match char in range

```
++  shim                                                ::  match char in range
  ~/  %shim
  |=  [les=@ mos=@]
  ~/  %fun
  |=  tub=nail
  ^-  (like char)
  ?~  q.tub
    (fail tub)
  ?.  ?&((gte i.q.tub les) (lte i.q.tub mos))
    (fail tub)
  (next tub)
::
```

Parser generator: produces a [rule]() that matches chars within the range between `les` and `mos`.

`les` is an [atom]().

`mos` is an [atom]().

`tub` is a [nail]().

    ~zod/try=> ((shim 'a' 'z') [[1 1] "abc"])
    [p=[p=1 q=2] q=[~ [p=~~a q=[p=[p=1 q=2] q="bc"]]]]
    ~zod/try=> ((shim 'a' 'Z') [[1 1] "abc"])
    [p=[p=1 q=1] q=~]
    ~zod/try=> ((shim 'a' 'Z') [[1 1] "Abc"])
    [p=[p=1 q=2] q=[~ [p=~~~41. q=[p=[p=1 q=2] q="bc"]]]]

---

###++stag

Add label

```
++  stag                                                ::  add a label
  ~/  %stag
  |*  [gob=* sef=_rule]
  ~/  %fun
  |=  tub=nail
  =+  vex=(sef tub)
  ?~  q.vex
    vex
  [p=p.vex q=[~ u=[p=[gob p.u.q.vex] q=q.u.q.vex]]]
::
```

Parser modifier: produces a rule that adds a label `gob` to an [edge]() parsed by `sef`.

        ~zod/try=> ((stag %foo (just 'a')) [[1 1] "abc"])
        [p=[p=1 q=2] q=[~ u=[p=[%foo ~~a] q=[p=[p=1 q=2] q="bc"]]]]
        ~zod/try=> ((stag "xyz" (jest 'abc')) [[1 1] "abc"])
        [p=[p=1 q=4] q=[~ u=[p=["xyz" 'abc'] q=[p=[p=1 q=4] q=""]]]]
        ~zod/try=> ((stag 10.000 (shim 0 100)) [[1 1] "abc"])
        [p=[p=1 q=2] q=[~ u=[p=[10.000 ~~a] q=[p=[p=1 q=2] q="bc"]]]]

---

###++stet

Add `[p q]` faces

```
++  stet
  |*  leh=(list ,[?(@ [@ @]) _rule])
  |-
  ?~  leh
    ~
  [i=[p=-.i.leh q=+.i.leh] t=$(leh t.leh)]
::
```

Produces list `leh` with the heads and tails of its elements assigned the faces `p` and `q` respectively. Used to prime input for [`++stew`]().

`leh` is a [list]() of elements that have two elements: `p`, which is either a character or a range of characters; and `q`, which is the corresponding [rule]().

    ~zod/try=> (stet (limo [[5 (just 'a')] [1 (jest 'abc')] [[1 1] (shim 0 200)] 
    [[1 10] (cold %foo (just 'a'))]~]))
    ~[
      [p=5 q=<1.lrk [tub=[p=[p=@ud q=@ud] q=""] <1.nqy [daf=@tD <394.imz 97.kdz 1.xlc %164>]>]>]
      [p=1 q=<1.lrk [tub=[p=[p=@ud q=@ud] q=""] <1.nqy [daf=@tD <394.imz 97.kdz 1.xlc %164>]>]>]
      [p=[1 1] q=<1.lrk [tub=[p=[p=@ud q=@ud] q=""] <1.nqy [daf=@tD <394.imz 97.kdz 1.xlc %164>]>]>]
      [p=[1 10] q=<1.lrk [tub=[p=[p=@ud q=@ud] q=""] <1.nqy [daf=@tD <394.imz 97.kdz 1.xlc %164>]>]>]
    ]
    ~zod/try=> [[[1 1] (just 'a')] [[2 1] (shim 0 200)] ~]
    [ [[1 1] <1.tnv [tub=[p=[p=@ud q=@ud] q=""] <1.ktu [daf=@tD <414.fvk 101.jzo 1.ypj %164>]>]>]
      [[2 1] <1.fvg [tub=[p=[p=@ud q=@ud] q=""] <1.khu [[les=@ mos=@] <414.fvk 101.jzo 1.ypj %164>]>]>]
      ~
    ]
    ~zod/try=> (stet (limo [[[1 1] (just 'a')] [[2 1] (shim 0 200)] ~]))
    ~[
      [p=[1 1] q=<1.lrk [tub=[p=[p=@ud q=@ud] q=""] <1.nqy [daf=@tD <394.imz 97.kdz 1.xlc %164>]>]>] 
      [p=[2 1] q=<1.lrk [tub=[p=[p=@ud q=@ud] q=""] <1.nqy [daf=@tD <394.imz 97.kdz 1.xlc %164>]>]>]
    ]

---

###++stew

Switch on first char

```
++  stew                                                ::  switch by first char
  ~/  %stew
  |*  leh=(list ,[p=?(@ [@ @]) q=_rule])                ::  char/range keys
  =+  ^=  wor                                           ::  range complete lth
      |=  [ort=?(@ [@ @]) wan=?(@ [@ @])]
      ?@  ort
        ?@(wan (lth ort wan) (lth ort -.wan))
      ?@(wan (lth +.ort wan) (lth +.ort -.wan))
  =+  ^=  hel                                           ::  build parser map
      =+  hel=`(tree $_(?>(?=(^ leh) i.leh)))`~
      |-  ^+  hel
      ?~  leh
        ~
      =+  yal=$(leh t.leh)
      |-  ^+  hel
      ?~  yal
        [i.leh ~ ~]
      ?:  (wor p.i.leh p.n.yal)
        =+  nuc=$(yal l.yal)
        ?>  ?=(^ nuc)
        ?:  (vor p.n.yal p.n.nuc)
          [n.yal nuc r.yal]
        [n.nuc l.nuc [n.yal r.nuc r.yal]]
      =+  nuc=$(yal r.yal)
      ?>  ?=(^ nuc)
      ?:  (vor p.n.yal p.n.nuc)
        [n.yal l.yal nuc]
      [n.nuc [n.yal l.yal l.nuc] r.nuc]
  ~%  %fun  ..^$  ~
  |=  tub=nail
  ?~  q.tub
    (fail tub)
  |-
  ?~  hel
    (fail tub)
  ?:  ?@  p.n.hel
        =(p.n.hel i.q.tub)
      ?&((gte i.q.tub -.p.n.hel) (lte i.q.tub +.p.n.hel))
    ::  (q.n.hel [(lust i.q.tub p.tub) t.q.tub])
    (q.n.hel tub)
  ?:  (wor i.q.tub p.n.hel)
    $(hel l.hel)
  $(hel r.hel)
::
```
   
Parser generator: produces a [rule]() that switches on the first character (by individual character or range), applying the corresponding [rule](). Used extensively in [`++norm`](), [`++toil`](), and [`++scat`]().

`ort` is a [list]() of elements that have two elements: `p`, which is either a character or a range of characters that are switched on; and `q` which is the corresponding [rule]().

---

###++stir

Parse repeatedly

```
++  stir                                                ::  parse repeatedly 
  ~/  %stir
  |*  [rud=* raq=_|*([a=* b=*] [a b]) fel=_rule]
  ~/  %fun
  |=  tub=nail
  ^-  (like ,_rud)
  =+  vex=(fel tub)
  ?~  q.vex
    [p.vex [~ rud tub]]
  =+  wag=$(tub q.u.q.vex)
  ?>  ?=(^ q.wag)
  [(last p.vex p.wag) [~ (raq p.u.q.vex p.u.q.wag) q.u.q.wag]]
::
```
        
Parser generator: produces a parser that parses with `fel` as many times as is possible and composes the results with a binary gate `raq`.

`rud` is a [noun]().

`raq` is a [gate]() that accepts a [cell]() of nouns `a` and `b` and produces a cell.

`fel` is a [rule]().

    ~zod/try=> (scan "abc" (stir *@ add prn))
    294
    ~zod/try=> (roll "abc" add)
    b=294

---
        
###++stun  

Parse several times

```
++  stun                                                ::  parse several times
  |*  [[les=@ mos=@] fel=_rule]
  |=  tub=nail
  ^-  (like (list ,_(wonk (fel))))
  ?:  =(0 mos)
    [p.tub [~ ~ tub]]
  =+  vex=(fel tub)
  ?~  q.vex
    ?:  =(0 les)
      [p.vex [~ ~ tub]]
    vex
  =+  ^=  wag  %=  $
                 les  ?:(=(0 les) 0 (dec les))
                 mos  ?:(=(0 mos) 0 (dec mos))
                 tub  q.u.q.vex
               ==
  ?~  q.wag
    wag
  [p.wag [~ [p.u.q.vex p.u.q.wag] q.u.q.wag]]
```

Parser generator: produces a rule that applies `fel` between `les` and `mos` times.

`les` is an [atom]().

`mos` is an [atom]().

`tub` is a [nail]().

    ~zod/try=> ((stun [5 10] prn) [1 1] "aquickbrownfoxran")
    [p=[p=1 q=11] q=[~ [p="aquickbrow" q=[p=[p=1 q=11] q="nfoxran"]]]]
    ~zod/try=> ((stun [5 10] prn) [1 1] "aquickbro")
    [p=[p=1 q=10] q=[~ [p="aquickbro" q=[p=[p=1 q=10] q=""]]]]
    ~zod/try=> ((stun [5 10] prn) [1 1] "aqui")
    [p=[p=1 q=5] q=~]

---
