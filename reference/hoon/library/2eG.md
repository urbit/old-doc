##section 2eG, parsing (whitespace)     

---

++  dog 

---

###++doh 

```
++  doh  ;~(plug ;~(plug hep hep) gay)                  ::
```

Parse 

---

###++dun

```
++  dun  (cold ~ ;~(plug hep hep))                      ::  -- (phep) to ~
```

Parse phep (--) to null (~).

        ~zod/try=> (scan "--" dun)
        ~
        ~zod/try=> (dun [[1 1] "--"])
        [p=[p=1 q=3] q=[~ u=[p=~ q=[p=[p=1 q=3] q=""]]]]

---

###++duz 

```
++  duz  (cold ~ ;~(plug tis tis))                      ::  == (stet) to ~
```

Parse stet (==) to null (~).

        ~zod/try=> (scan "==" duz)
        ~
        ~zod/try=> (duz [[1 1] "== |=..."])
        [p=[p=1 q=3] q=[~ u=[p=~ q=[p=[p=1 q=3] q=" |=..."]]]]

---

###++gah 

```
++  gah  (mask [`@`10 ' ' ~])                           ::  newline or ace
```

---

###++gap 

```
++  gap  (cold ~ ;~(plug gaq (star ;~(pose vul gah))))  ::
```
        
---

---

###++gaq

```
++  gaq  ;~  pose                                       ::  end of line
             (just `@`10)
             ;~(plug gah ;~(pose gah vul))
             vul
         ==
```

---
        
###++gay 

```
++  gay  ;~(pose gap (easy ~))                          ::
```
        
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

---


