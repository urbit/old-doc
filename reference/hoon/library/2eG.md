section 2eG, parsing (whitespace)     

---

++  dog 

---

###++doh 

```
++  doh  ;~(plug ;~(plug hep hep) gay)                  ::
```

Parse 

####Summary

        Produce plug gonadified with dot and gay.

####Examples

---

###++dun

```
++  dun  (cold ~ ;~(plug hep hep))                      ::  -- (phep) to ~
```

Parse phep (--) to null (~).

####Summary

        Produce cold slammed with:
                null
                plug gonadified with hep and hep, to parse phep.

####Examples

        ~tadbyl-hilbel/try=> (scan "--" dun)
        ~
        ~tadbyl-hilbel/try=> (dun [[1 1] "--"])
        [p=[p=1 q=3] q=[~ u=[p=~ q=[p=[p=1 q=3] q=""]]]]

---

###++duz 

```
++  duz  (cold ~ ;~(plug tis tis))                      ::  == (stet) to ~
```

Parse stet (==) to null (~).

####Summary

        Produce cold slammed with:
                null
                plug gonadified with tis and tis, to parse stet

####Examples

        ~tadbyl-hilbel/try=> (scan "==" duz)
        ~
        ~tadbyl-hilbel/try=> (duz [[1 1] "== |=..."])
        [p=[p=1 q=3] q=[~ u=[p=~ q=[p=[p=1 q=3] q=" |=..."]]]]

---

###++gah 

```
++  gah  (mask [`@`10 ' ' ~])                           ::  newline or ace
```

####Summary

        Produce mask slammed with the tuple:
                `@`10, the newline character
                ' ', the ace character
                null

####Examples

---

###++gap 

```
++  gap  (cold ~ ;~(plug gaq (star ;~(pose vul gah))))  ::
```
        
---

####Summary

        Produce cold slammed with:
                null
                Plug gonadified with:
                        gaq
                        star slammed with pose gonadified with vul and gah

###Examples

---

###++gaq

```
++  gaq  ;~  pose                                       ::  end of line
             (just `@`10)
             ;~(plug gah ;~(pose gah vul))
             vul
         ==
```

####Summary

        Produce pose gonadifed with:
                just slammed with the newline character.
                Plug gonadified with gah and pose gonadified with gah and vul.
                vul

####Examples

---
        
###++gay 

```
++  gay  ;~(pose gap (easy ~))                          ::
```
        
####Summary

        Produce pose gonadified with:
                gap, which
                Slam of easy with null

####Examples

---
        
###++vul 

```
++  vul  %-  cold  :-  ~                                ::  comments
         ;~  plug  col  col
           (star prn)
           (just `@`10)
         ==
```

Parse comments and replace them with null.
Note that a comment must be ended with a newline character.

####Summary

        Produce cold slammed with: Pair null and,
                plug gonadified with col, col, and,
                        pose gonadified with:
                                shim slammed with 32 and 126
                                shim slammed with 128 and 255
                                just slammed with the newline operator.
        (==) Terminates the pair.

####Examples

---


