##section 2eE, parsing (composers)

---

###++bass

```
++  bass
  |*  [wuc=@ tyd=_rule]
  %+  cook
    |=  waq=(list ,@)
    %+  roll
      waq
    =|([p=@ q=@] |.((add p (mul wuc q))))
  tyd
::
```

---

###++boss

```
++  boss
  |*  [wuc=@ tyd=_rule]
  %+  cook
    |=  waq=(list ,@)
    %+  reel
      waq
    =|([p=@ q=@] |.((add p (mul wuc q))))
  tyd
::
```

---

###++ifix

```
++  ifix
  |*  [fel=[p=_rule q=_rule] hof=_rule]
  ;~(pfix p.fel ;~(sfix hof q.fel))
::
```
        
---
        
###++more

```
++  more
  |*  [bus=_rule fel=_rule]
  ;~(pose (most bus fel) (easy ~))
::
```

---

###++most

```
++  most
  |*  [bus=_rule fel=_rule]
  ;~(plug fel (star ;~(pfix bus fel)))
::
```

Parse to a list elements of the second rule seperated by the second.

---
        
###++plus  

```
++  plus  |*(fel=_rule ;~(plug fel (star fel)))
```

Like 'star', but "one or more" instead of "0 or more"

---
        
###++slug

```
++  slug
  |*  [rud=* raq=_|*([a=* b=*] [a b])]
  |*  [bus=_rule fel=_rule]
  ;~((comp raq) fel (stir rud raq ;~(pfix bus fel)))
::
```

---
        
###++star

```
++  star                                                ::  0 or more times
  |*  fel=_rule
  (stir `(list ,_(wonk *fel))`~ |*([a=* b=*] [a b]) fel)
```

Apply the parsing rule repeatedly until it fails.


        ~zod/try=> (scan "aaaaa" (just 'a'))
        ! {1 2}
        ! 'syntax-error'
        ! exit
        ~zod/try=> (scan "aaaaa" (star (just 'a')))
        "aaaaa"
        ~zod/try=> (scan "abcdef" (star (just 'a')))
        ! {1 2}
        ! 'syntax-error'
        ! exit
        ~zod/try=> (scan "abcabc" (star (jest 'abc')))
        <|abc abc|>
        ~zod/try=> (scan "john smith" (star (shim 0 200)))
        "john smith"

---


