section 2eH, parsing (idioms)         

###++alf 

```
++  alf  ;~(pose low hig)                               ::  alphabetic
```

Parse alphabetic characters, both upper and lowercase.

####Summary

        Produce the rule of pose gonadified with low and hig.

####Examples

        ~tadbyl-hilbel/try=> (scan "a" alf)
        ~~a
        ~tadbyl-hilbel/try=> (scan "A" alf)
        ~~~41.
        ~tadbyl-hilbel/try=> (scan "AaBbCc" (star alf))
        "AaBbCc"

###++aln 

```
++  aln  ;~(pose low hig nud)                           ::  alphanumeric
```

Parse alphanumeric characters - both alphabetic characters and numbers.

####Summary

        Produce the rule of pose gonadified with low,hig, and nud.

####Examples

        ~tadbyl-hilbel/try=> (scan "0" aln)
        ~~0
        ~tadbyl-hilbel/try=> (scan "alf42" (star aln))
        "alf42"
        ~tadbyl-hilbel/try=> (scan "0123456789abcdef" (star aln))
        "0123456789abcdef"

###++alp 

```
++  alp  ;~(pose low hig nud hep)                       ::  alphanumeric and -
```

Parse alphanumeric strings and hep, "-".

####Summary

        Produce the rule pose gonadified with low, hig, nud, hep.

####Examples

        ~tadbyl-hilbel/try=> (scan "7" alp)
        ~~7
        ~tadbyl-hilbel/try=> (scan "s" alp)
        ~~s
        ~tadbyl-hilbel/try=> (scan "123abc-" (star alp))
        "123abc-"

###++bet 

```
++  bet  ;~(pose (cold 2 hep) (cold 3 lus))             ::  axis syntax - +
```

Parse the hep and lus axis syntax.


####Summary

        Produce the rule pose gonadified with:
                        (cold 2 hep), which replaces parsed heps with 2s.
                        (cold 3 lus), which replaced parsed luses with 3s.

####Examples

        ~tadbyl-hilbel/try=> (scan "-" bet)
        2
        ~tadbyl-hilbel/try=> (scan "+" bet)
        3

###++bin

```
++  bin  (bass 2 (most gon but))                        ::  binary to atom
```

Parse a tape of binary (0s and 1s) and produce its atomic representation.

####Summary

        Produce the slam of bass with 2 and the (most gon but), which produces 

####Examples
        
        ~tadbyl-hilbel/try=> (scan "0000" bin)
        0
        ~tadbyl-hilbel/try=> (scan "0001" bin)
        1
        ~tadbyl-hilbel/try=> (scan "0010" bin)
        2
        ~tadbyl-hilbel/try=> (scan "100000001111" bin)
        2.063

###++but 

```
++  but  (cook |=(a=@ (sub a '0')) (shim '0' '1'))      ::  binary digit
```

Parse a single binary digit.

####Summary

        Produce rule cook slammed with a gate:
                With sample atom `a` that results in the difference between `a` and '0' (48).
                        All slammed with the rule shim slammed with '0' and '1', to parse either of those characters.

####Examples

        ~tadbyl-hilbel/try=> (scan "0" but)
        0
        ~tadbyl-hilbel/try=> (scan "1" but)
        1
        ~tadbyl-hilbel/try=> (scan "01" but)
        ! {1 2}
        ! 'syntax-error'
        ! exit
        ~tadbyl-hilbel/try=> (scan "01" (star but))
        ~[0 1]

###++cit 

```
++  cit  (cook |=(a=@ (sub a '0')) (shim '0' '7'))      ::  octal digit
```

Parse a single octal digit.

####Summary

        Produce rule cook slammed with a gate:
                With sample atom `a` that results in the difference between `a` and '0' (48).
                        All slammed with the rule shim slammed with '0' and '7', to parse any number between 0 and 7.

####Examples

        ~tadbyl-hilbel/try=> (scan "1" cit)
        1
        ~tadbyl-hilbel/try=> (scan "7" cit)
        7
        ~tadbyl-hilbel/try=> (scan "8" cit)
        ! {1 1}
        ! 'syntax-error'
        ! exit
        ~tadbyl-hilbel/try=> (scan "60" (star cit))
        ~[6 0]

###++dem 

```
++  dem  (bass 10 (most gon dit))                       ::  decimal to atom
```

Parse a decimal number to an atom.

####Summary

        Produce the slam of bass with 10 (The base number system) and (most gon dit), which produces 
        
####Examples

        ~tadbyl-hilbel/try=> (scan "7" dem)
        7
        ~tadbyl-hilbel/try=> (scan "42" dem)
        42
        ~tadbyl-hilbel/try=> (scan "150000000" dem)
        150.000.000
        ~tadbyl-hilbel/try=> (scan "12456" dem)
        12.456

###++dit 

```
++  dit  (cook |=(a=@ (sub a '0')) (shim '0' '9'))      ::  decimal digit
```

 Parse a single decimal digit.

####Summary

        Produce the rule cook slammed with a gate:
                With sample atom `a` that results in the difference between `a` and '0' (48).
                        All slammed with the rule shim slammed with '0' and '9', to parse any number.

####Examples

        ~tadbyl-hilbel/try=> (scan "7" dit)
        7
        ~tadbyl-hilbel/try=> (scan "42" (star dit))
        ~[4 2]
        ~tadbyl-hilbel/try=> (scan "26000" (star dit))
        ~[2 6 0 0 0]

###++gul 

```
++  gul  ;~(pose (cold 2 gal) (cold 3 gar))             ::  axis syntax < >
```

Parse the axis gal and gar axis syntax.

####Summary

        Produce the rule pose gonadified with:
                (cold 2 gal), which replaces parsed gals with 2s.
                (cold 3 gar), which replaced parsed gars with 3s.

####Examples

        ~tadbyl-hilbel/try=> (scan "<" gul)
        2
        ~tadbyl-hilbel/try=> (scan ">" gul)
        3

###++gon 

```
++  gon  ;~(pose ;~(plug bas gay fas) (easy ~))         ::  long numbers \ /
```

Parse long numbers - Numbers which wrap around the shell with the line break characters bas and fas.

####Summary

        Produce the rule pose gonadified with:
                The rule plug gonadified with:
                        bas, gay, and fas, to succeed to parse a bas, fas, or a gap in text.
                The rule (easy ~), to succeed to parse but produces null as the parsed text.

####Examples

        ~tadbyl-hilbel/try=> (scan "\\/" gon)
        [~~~5c. ~ ~~~2f.]
        ~tadbyl-hilbel/try=> (gon [[1 1] "\\/"])
        [p=[p=1 q=3] q=[~ u=[p=[~~~5c. ~ ~~~2f.] q=[p=[p=1 q=3] q=""]]]]

###++hex 

```
++  hex  (bass 16 (most gon hit))                       ::  hex to atom
```

Parse any hexadecimal number to an atom.

####Summary

        Produce bass slammed with 16 (The base number system) and (most gon hit), which produces the atom 

####Examples

        ~tadbyl-hilbel/try=> (scan "a" hex)
        10
        ~tadbyl-hilbel/try=> (scan "A" hex)
        10
        ~tadbyl-hilbel/try=> (scan "2A" hex)
        42
        ~tadbyl-hilbel/try=> (scan "1ee7" hex)
        7.911
        ~tadbyl-hilbel/try=> (scan "1EE7" hex)
        7.911

###++hig

```
++  hig  (shim 'A' 'Z')                                 ::  uppercase
```

Parse a single uppercase letter.

####Summary

        Produce the slam of shim with the characters 'A' (65) and 'Z' (90), to parse any character between them, inclusive.

####Examples

        ~tadbyl-hilbel/try=> (scan "G" hig)
        ~~~47.
        ~tadbyl-hilbel/try=> `cord`(scan "G" hig)
        'G'
        ~tadbyl-hilbel/try=> (scan "ABCDEFGHIJKLMNOPQRSTUVWXYZ" (star hig))
        "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
        ~tadbyl-hilbel/try=> (hig [[1 1] "G"])
        [p=[p=1 q=2] q=[~ [p=~~~47. q=[p=[p=1 q=2] q=""]]]]

###++hit 

```
++  hit  ;~  pose                                       ::  hex digits
           dit
           (cook |=(a=char (sub a 87)) (shim 'a' 'f'))
           (cook |=(a=char (sub a 55)) (shim 'A' 'F'))
         ==
```

Parse a single hexadecimal digit.

####Summary

        Pose gonadified with:
                dit, parse a single decimnal digit.
                Slam cook with:
                        Build dry %gold gate with sample char `a`.  Produce the difference between `a` and 87.
                        The slam of shim with the characters 'a' (97) and 'z' (122), to parse any character between them, inclusive.
                        The slam of shim with the characters 'A' () and 'Z' (), to parse any character between them, inclusive.
        Terminate the gonadification.

####Examples

        ~tadbyl-hilbel/try=> (scan "a" hit)
        10
        ~tadbyl-hilbel/try=> (scan "A" hit)
        10
        ~tadbyl-hilbel/try=> (hit [[1 1] "a"])
        [p=[p=1 q=2] q=[~ [p=10 q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (scan "2A" (star hit))
        ~[2 10]

###++low 

```
++  low  (shim 'a' 'z')                                 ::  lowercase
```

Parse a single lowercase letter.

####Summary        

        Produce the slam of shim with the characters 'a' (97) and 'z' (122), to parse any character between them, inclusive.

####Examples

        ~tadbyl-hilbel/try=> (scan "g" low)
        ~~g
        ~tadbyl-hilbel/try=> `cord`(scan "g" low)
        'g'
        ~tadbyl-hilbel/try=> (scan "abcdefghijklmnopqrstuvwxyz" (star low))
        "abcdefghijklmnopqrstuvwxyz"
        ~tadbyl-hilbel/try=> (low [[1 1] "g"])
        [p=[p=1 q=2] q=[~ [p=~~g q=[p=[p=1 q=2] q=""]]]]

###++mes 

```
++  mes  %+  cook                                       ::  hexbyte
           |=([a=@ b=@] (add (mul 16 a) b))
         ;~(plug hit hit)
```

Parse a hexbyte.

####Sumamry

        Slam cook with:
                Build dry %gold gate with sample atom `a`, atom `b`.  Produce the sum of `a` multiplied by 16 and `b`
                Plug gonadified with hit and hit, parse two consecutive hex digits.
####Examples

        ~tadbyl-hilbel/try=> (scan "2A" mes)
        42
        ~tadbyl-hilbel/try=> (mes [[1 1] "2A"])
        [p=[p=1 q=3] q=[~ u=[p=42 q=[p=[p=1 q=3] q=""]]]]
        ~tadbyl-hilbel/try=> (scan "42" mes)
        66

###++nix 

```
++  nix  (boss 256 (star ;~(pose aln cab)))             ::
```

Letters, -, and _
        
###++nud 

Parse a numeric character - A number.

####Summary

        Produce the slam of shim with the characters '0' (48) and '9' (57), to parse  any character between them, inclusive.

####Examples

        ~tadbyl-hilbel/try=> (scan "0" nud)
        ~~0
        ~tadbyl-hilbel/try=> (scan "7" nud)
        ~~7
        ~tadbyl-hilbel/try=> (nud [[1 1] "1"])
        [p=[p=1 q=2] q=[~ [p=~~1 q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (scan "0123456789" (star nud))
        "0123456789"
        
###++qit 

```
++  qit  ;~  pose                                       ::  chars in a cord
             ;~(less bas soq prn)
             ;~(pfix bas ;~(pose bas soq mes))          ::  escape chars
         ==
```

Parse an individual character to its cord atom representation.

####Summary

        Produce pose gonadified with:
                The slam of shim with 32 and 38, to parse any characters between them, inclusive.
                The slam of shim with 40 and 91, to parse any characters between them, inclusive.
                The slam of shim with 93 and 126, to parse any characters between them, inclusive.
                The slam of shim with 128 and 255, to parse any characters between them, inclusive.

####Examples

        ~tadbyl-hilbel/try=> (scan "%" qit)
        37
        ~tadbyl-hilbel/try=> (scan "0" qit)
        48
        ~tadbyl-hilbel/try=> (scan "E" qit)
        69
        ~tadbyl-hilbel/try=> (scan "a" qit)
        97
        ~tadbyl-hilbel/try=> (scan "cord" (star qit))
        ~[99 111 114 100]

###++qut 

```
++  qut  ;~  pose                                       ::  cord
             ;~  less  soqs
               (ifix [soq soq] (boss 256 (more gon qit)))
             ==
             %-  inde  %+  ifix
               :-  ;~  plug  soqs
                     ;~(pose ;~(plug (plus ace) vul) (just '\0a'))
                   ==
               ;~(plug (just '\0a') soqs)
             (boss 256 (star qat))
         ==
::
```

Parse 

####Summary

        Slam ifix with:
                [soq soq]
                boss slammed with 256 and (most gon qit)
        

###++sym

```
++  sym
  %+  cook
    |=(a=tape (rap 3 ^-((list ,@) a)))
  ;~(plug low (star ;~(pose nud low hep)))
::
```
        

###++ven 


###++vit 

```
++  vit                                                 ::  base64 digit
  ;~  pose
    (cook |=(a=@ (sub a 65)) (shim 'A' 'Z'))
    (cook |=(a=@ (sub a 71)) (shim 'a' 'z'))
    (cook |=(a=@ (add a 4)) (shim '0' '9'))
    (cold 62 (just '-'))
    (cold 63 (just '+'))
  ==
```

Parse a text and produce its base 64 encoding

####Summary

        Build list of falling rules to match on with ';~' and pose.
        Encodes capital letters by 


