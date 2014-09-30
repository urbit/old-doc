section 2eE, parsing (composers)

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

####Summary

        Build wet %gold gate with sample atom `wuc`, rule `tyd`
        Slam cook with:
                Build dry %gold gate with sample list of atoms, `waq`
                Slam roll with:
###Examples

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

####Summary

        Build wet %gold gate with sample atom `wuc`, rule `tyd`

####Examples

---

###++ifix

```
++  ifix
  |*  [fel=[p=_rule q=_rule] hof=_rule]
  ;~(pfix p.fel ;~(sfix hof q.fel))
::
```
        
####Summary

        Build wet %gold gate with sample cell of rules `fel`, rule `hof`
        Produce pfix gonadified with:
            `p.fel`, the first rule in `fel`
            Gonadify sfix with `hof` and `q.fel`, the second rule in `fel`

####Examples

---
        
###++more

```
++  more
  |*  [bus=_rule fel=_rule]
  ;~(pose (most bus fel) (easy ~))
::
```

####Summary

        Build wet %gold gate with sample rule `bus`, rule `fel`
        Produce the gonadified:

###Examples

---

###++most

```
++  most
  |*  [bus=_rule fel=_rule]
  ;~(plug fel (star ;~(pfix bus fel)))
::
```

Parse to a list elements of the second rule seperated by the second.

####Summary

        Build wet %gold gate with sample rule `bus`, rule `fel`
        Produce gonadified:
                Plug slammed with `fel`,
                        star slammed with gonadified:
                                pfix slammed with `bus` and `fel`, `bus` added as the prefix of `fel`
###Examples

---
        
###++plus  

```
++  plus  |*(fel=_rule ;~(plug fel (star fel)))
```

Like 'star', but "one or more" instead of "0 or more"

####Summary

        Build wet %gold gate with sample rule `fel`
        Produce gonadified:
                plug slammed with `fel` and star slammed with `fel`, the repeated application of `fel`.

####Examples

---
        
###++slug

```
++  slug
  |*  [rud=* raq=_|*([a=* b=*] [a b])]
  |*  [bus=_rule fel=_rule]
  ;~((comp raq) fel (stir rud raq ;~(pfix bus fel)))
::
```

####Summary

        Build wet %gold gate with sample noun `rud`, gate accepting  cell of two nouns and producing [a b] `raq`
        Build wet %gold gate with sample rule `bus`, rule `fel`
        Produce the gonadified:
                comp slammed with `raq`, 
                        slammed with `fel`, 
                                slammed with,
                                        stir slammed with `rud`, `raq`, and `fel` prefixed with `bus`
####Examples

---
        
###++star

```
++  star                                                ::  0 or more times
  |*  fel=_rule
  (stir `(list ,_(wonk *fel))`~ |*([a=* b=*] [a b]) fel)
```

Apply the parsing rule repeatedly until it fails.

####Summary

        Build wet %gold gate with sample rule `fel,
        Produce stir slammed with:
                The list of elements of type of the icon of `fel` slammed to `wonk`
        

####Examples

        ~tadbyl-hilbel/try=> (scan "aaaaa" (just 'a'))
        ! {1 2}
        ! 'syntax-error'
        ! exit
        ~tadbyl-hilbel/try=> (scan "aaaaa" (star (just 'a')))
        "aaaaa"
        ~tadbyl-hilbel/try=> (scan "abcdef" (star (just 'a')))
        ! {1 2}
        ! 'syntax-error'
        ! exit
        ~tadbyl-hilbel/try=> (scan "abcabc" (star (jest 'abc')))
        <|abc abc|>
        ~tadbyl-hilbel/try=> (scan "john smith" (star (shim 0 200)))
        "john smith"

---


