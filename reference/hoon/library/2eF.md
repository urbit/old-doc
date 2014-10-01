section 2eF, parsing (ascii)          

---

###++ace

```
++  ace  (just ' ')                                     ::  spACE
```

Parse ASCII character 32, ace.

###Examples

        ~tadbyl-hilbel/try=> (scan " " ace)
        ~~. 
        ~tadbyl-hilbel/try=> `cord`(scan " " ace)
        ' '
        ~tadbyl-hilbel/try=> (ace [[1 1] " "])
        [p=[p=1 q=2] q=[~ [p=~~. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (ace [[1 1] " abc "])
        [p=[p=1 q=2] q=[~ [p=~~. q=[p=[p=1 q=2] q="abc "]]]]

---

###++bar 

```
++  bar  (just '|')                                     ::  vertical BAR
```

Parse ASCII character 124, bar.

####Examples

       ~tadbyl-hilbel/try=> (scan "|" bar)
        ~~~7c. 
        ~tadbyl-hilbel/try=> `cord`(scan "|" bar)
        '|'
        ~tadbyl-hilbel/try=> (bar [[1 1] "|"])
        [p=[p=1 q=2] q=[~ [p=~~~7c. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (bar [[1 1] "|="])
        [p=[p=1 q=2] q=[~ [p=~~~7c. q=[p=[p=1 q=2] q="="]]]]

---

###++bas 

```
++  bas  (just '\\')                                    ::  Back Slash (escaped)
```

Parse ASCII character 92, bas.
Note the extra '\' in the slam of bas with just is to escape the escape character, bas.

###Examples

        ~tadbyl-hilbel/try=> (scan "\\" bas)
        ~~~5c.
        ~tadbyl-hilbel/try=> `cord`(scan "\\" bas)
        '\'
        ~tadbyl-hilbel/try=> (bas [[1 1] "\"])
        ~ <syntax error at [1 18]>
        ~tadbyl-hilbel/try=> (bas [[1 1] "\\"])
        [p=[p=1 q=2] q=[~ [p=~~~5c. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (bas [[1 1] "\""])
        [p=[p=1 q=1] q=~]

---

###++buc 

```
++  buc  (just '$')                                     ::  dollars BUCks
```

Parse ASCII character 36, buc.

####Examples

        ~tadbyl-hilbel/try=> (scan "$" buc)
        ~~~24.
        ~tadbyl-hilbel/try=> `cord`(scan "$" buc)
        '$'
        ~tadbyl-hilbel/try=> (buc [[1 1] "$"])
        [p=[p=1 q=2] q=[~ [p=~~~24. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (buc [[1 1] "$%"])
        [p=[p=1 q=2] q=[~ [p=~~~24. q=[p=[p=1 q=2] q="%"]]]]

---

###++cab 

```
++  cab  (just '_')                                     ::  CABoose
```

Parse ASCII character 95, cab.

###Examples

        ~tadbyl-hilbel/try=> (scan "_" cab)
        ~~~5f.
        ~tadbyl-hilbel/try=> `cord`(scan "_" cab)
        '_'
        ~tadbyl-hilbel/try=> (cab [[1 1] "_"])
        [p=[p=1 q=2] q=[~ [p=~~~5f. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (cab [[1 1] "|_"])
        [p=[p=1 q=1] q=~]

---

###++cen 

```
++  cen  (just '%')                                     ::  perCENt
```

Parse ASCII character 37, cen.

####Examples

        ~tadbyl-hilbel/try=> (scan "%" cen)
        ~~~25.
        ~tadbyl-hilbel/try=> `cord`(scan "%" cen)
        '%'
        ~tadbyl-hilbel/try=> (cen [[1 1] "%"])
        [p=[p=1 q=2] q=[~ [p=~~~25. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (cen [[1 1] "%^"])
        [p=[p=1 q=2] q=[~ [p=~~~25. q=[p=[p=1 q=2] q="^"]]]] 

---

###++col 

```
++  col  (just ':')                                     ::  COLon
```

Parse ASCII character 58, col.

###Examples

        ~tadbyl-hilbel/try=> (scan ":" col)
        ~~~3a.
        ~tadbyl-hilbel/try=> `cord`(scan ":" col)
        ':'
        ~tadbyl-hilbel/try=> (col [[1 1] ":"])
        [p=[p=1 q=2] q=[~ [p=~~~3a. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (col [[1 1] ":-"])
        [p=[p=1 q=2] q=[~ [p=~~~3a. q=[p=[p=1 q=2] q="-"]]]]

---

###++com 

```
++  com  (just ',')                                     ::  COMma
```

Parse ASCII character 44, com.

####Examples

        ~tadbyl-hilbel/try=> (scan "," com)
        ~~~2c.
        ~tadbyl-hilbel/try=> `cord`(scan "," com)
        ','
        ~tadbyl-hilbel/try=> (com [[1 1] ","])
        [p=[p=1 q=2] q=[~ [p=~~~2c. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (com [[1 1] "not com"])
        [p=[p=1 q=1] q=~]

---

###++doq 

```
++  doq  (just '"')                                     ::  Double Quote
```

Parse ASCII character 34, doq.

       ~tadbyl-hilbel/try=> (scan "\"" doq)
        ~~~22.
        ~tadbyl-hilbel/try=> `cord`(scan "\"" doq)
        '"'
        ~tadbyl-hilbel/try=> (doq [[1 1] "\""])
        [p=[p=1 q=2] q=[~ [p=~~~22. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (doq [[1 1] "not successfully parsed"])
        [p=[p=1 q=1] q=~]
        ~tadbyl-hilbel/try=> (scan "see?" doq)
        ! {1 1}
        ! 'syntax-error'
        ! exit 

---

###++dot 

```
++  dot  (just '.')                                     ::  dot dot dot ...
```

Parse ASCII character 46, dot.

####Examples

        ~tadbyl-hilbel/try=> (scan "." dot)
        ~~~.
        ~tadbyl-hilbel/try=> `cord`(scan "." dot)
        '.'
        ~tadbyl-hilbel/try=> (dot [[1 1] "."])
        [p=[p=1 q=2] q=[~ [p=~~~. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (dot [[1 1] ".^"])
        [p=[p=1 q=2] q=[~ [p=~~~. q=[p=[p=1 q=2] q="^"]]]]

---

###++fas 

```
++  fas  (just '/')                                     ::  Forward Slash
```

Parse ASCII character 47, fas.

###Examples

        ~tadbyl-hilbel/try=> (scan "/" fas)
        ~~~2f.
        ~tadbyl-hilbel/try=> `cord`(scan "/" fas)
        '/'
        ~tadbyl-hilbel/try=> (fas [[1 1] "/"])
        [p=[p=1 q=2] q=[~ [p=~~~2f. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (fas [[1 1] "|/"])
        [p=[p=1 q=1] q=~]

---

###++gal 

```
++  gal  (just '<')                                     ::  Greater Left
```

Parse ASCII character 60, gal.

####Examples

        ~tadbyl-hilbel/try=> (scan "<" gal)
        ~~~3c.
        ~tadbyl-hilbel/try=> `cord`(scan "<" gal)
        '<'
        ~tadbyl-hilbel/try=> (gal [[1 1] "<"])
        [p=[p=1 q=2] q=[~ [p=~~~3c. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (gal [[1 1] "<+"])
        [p=[p=1 q=2] q=[~ [p=~~~3c. q=[p=[p=1 q=2] q="+"]]]]
        ~tadbyl-hilbel/try=> (gal [[1 1] "+<"])
        [p=[p=1 q=1] q=~]

---

###++gar 

```
++  gar  (just '>')                                     ::  Greater Right
```

Parse ASCII character 62, gar.

####Examples

        ~tadbyl-hilbel/try=> (scan ">" gar)
        ~~~3e.
        ~tadbyl-hilbel/try=> `cord`(scan ">" gar)
        '>'
        ~tadbyl-hilbel/try=> (gar [[1 1] ">"])
        [p=[p=1 q=2] q=[~ [p=~~~3e. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (gar [[1 1] "=>"])
        [p=[p=1 q=1] q=~]

---

###++hax 

```
++  hax  (just '#')                                     ::  Hash
```

Parse ASCII character 35, hax.

####Examples

        ~tadbyl-hilbel/try=> (scan "#" hax)
        ~~~23.
        ~tadbyl-hilbel/try=> `cord`(scan "#" hax)
        '#'
        ~tadbyl-hilbel/try=> (hax [[1 1] "#"])
        [p=[p=1 q=2] q=[~ [p=~~~23. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (hax [[1 1] "#!"])
        [p=[p=1 q=2] q=[~ [p=~~~23. q=[p=[p=1 q=2] q="!"]]]]

---

###++kel 

```
++  kel  (just '{')                                     ::  Curly Left
```

Parse ASCII character 123, kel.
Note that this, with ker, opens and closes a Hoon expression for Hoon string interpolation.  Escape kel to parse it.

####Examples

        ~tadbyl-hilbel/try=> (scan "\{" kel)
        ~~~7b.
        ~tadbyl-hilbel/try=> `cord`(scan "\{" kel)
        '{'
        ~tadbyl-hilbel/try=> (kel [[1 1] "\{"])
        [p=[p=1 q=2] q=[~ [p=~~~7b. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (kel [[1 1] " \{"])
        [p=[p=1 q=1] q=~]

---

###++ker 

```
++  ker  (just '}')                                     ::  Curly Right
```

Parse ASCII character 125, ker.

###Examples

        ~tadbyl-hilbel/try=> (scan "}" ker)
        ~~~7d.
        ~tadbyl-hilbel/try=> `cord`(scan "}" ker)
        '}'
        ~tadbyl-hilbel/try=> (ker [[1 1] "}"])
        [p=[p=1 q=2] q=[~ [p=~~~7d. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (ker [[1 1] "\{}"])
        [p=[p=1 q=1] q=~]

---

###++ket 

```
++  ket  (just '^')                                     ::  CareT
```

Parse ASCII character 94, ket.

####Examples

        ~tadbyl-hilbel/try=> (scan "^" ket)
        ~~~5e.
        ~tadbyl-hilbel/try=> `cord`(scan "^" ket)
        '^'
        ~tadbyl-hilbel/try=> (ket [[1 1] "^"])
        [p=[p=1 q=2] q=[~ [p=~~~5e. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (ket [[1 1] ".^"])
        [p=[p=1 q=1] q=~]

---

###++lus 

```
++  lus  (just '+')                                     ::  pLUS
```

Parse ASCII character 43, lus.

###Examples

        ~tadbyl-hilbel/try=> (scan "+" lus)
        ~~~2b.
        ~tadbyl-hilbel/try=> `cord`(scan "+" lus)
        '+'
        ~tadbyl-hilbel/try=> (lus [[1 1] "+"])
        [p=[p=1 q=2] q=[~ [p=~~~2b. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (lus [[1 1] ".+"])
        [p=[p=1 q=1] q=~]

---

###++hep 

```
++  hep  (just '-')                                     ::  HyPhen
```

Parse ASCII character 45, hep.

####Examples

        ~tadbyl-hilbel/try=> (scan "-" hep)
        ~~-
        ~tadbyl-hilbel/try=> `cord`(scan "-" hep)
        '-'
        ~tadbyl-hilbel/try=> (hep [[1 1] "-"])
        [p=[p=1 q=2] q=[~ [p=~~- q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (hep [[1 1] ":-"])
        [p=[p=1 q=1] q=~]

---

###++pel 

```
++  pel  (just '(')                                     ::  Paren Left
```

Parse ASCII character 40, pel.

####Examples

        ~tadbyl-hilbel/try=> (scan "(" pel)
        ~~~28.
        ~tadbyl-hilbel/try=> `cord`(scan "(" pel)
        '('
        ~tadbyl-hilbel/try=> (pel [[1 1] "("])
        [p=[p=1 q=2] q=[~ [p=~~~28. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (pel [[1 1] ";("])
        [p=[p=1 q=1] q=~]

---

###++pam 

```
++  pam  (just '&')                                     ::  AMPersand pampersand
```

Parse ASCII character 38, pam.

####Examples

        ~tadbyl-hilbel/try=> (scan "&" pam)
        ~~~26.
        ~tadbyl-hilbel/try=> `cord`(scan "&" pam)
        '&'
        ~tadbyl-hilbel/try=> (pam [[1 1] "&"])
        [p=[p=1 q=2] q=[~ [p=~~~26. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (pam [[1 1] "?&"])
        [p=[p=1 q=1] q=~]

---

###++per 

```
++  per  (just ')')                                     ::  Paren Right
```

Parse ASCII character 41, per.

###Examples

        ~tadbyl-hilbel/try=> (scan ")" per)
        ~~~29.
        ~tadbyl-hilbel/try=> `cord`(scan ")" per)
        ')'
        ~tadbyl-hilbel/try=> (per [[1 1] ")"])
        [p=[p=1 q=2] q=[~ [p=~~~29. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (per [[1 1] " )"])
        [p=[p=1 q=1] q=~]

---

###++pat 

```
++  pat  (just '@')                                     ::  AT pat
```

Parse ASCII character 64, pat.

####Examples

        ~tadbyl-hilbel/try=> (scan "@" pat)
        ~~~4.
        ~tadbyl-hilbel/try=> `cord`(scan "@" pat)
        '@'
        ~tadbyl-hilbel/try=> (pat [[1 1] "@"])
        [p=[p=1 q=2] q=[~ [p=~~~4. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (pat [[1 1] "?@"])
        [p=[p=1 q=1] q=~]

---

###++sel

```
++  sel  (just '[')                                     ::  Square Left
```

Parse ASCII character 91, sel.

####Examples

        ~tadbyl-hilbel/try=> (scan "[" sel)
        ~~~5b.
        ~tadbyl-hilbel/try=> `cord`(scan "[" sel)
        '['
        ~tadbyl-hilbel/try=> (sel [[1 1] "["])
        [p=[p=1 q=2] q=[~ [p=~~~5b. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (sel [[1 1] "-["])
        [p=[p=1 q=1] q=~]

---

###++sem 

```
++  sem  (just ';')                                     ::  SEMicolon
```

Parse ASCII character 59, sem.

###Exampels

        ~tadbyl-hilbel/try=> (scan ";" sem)
        ~~~3b.
        ~tadbyl-hilbel/try=> `cord`(scan ";" sem)
        ';'
        ~tadbyl-hilbel/try=> (sem [[1 1] ";"])
        [p=[p=1 q=2] q=[~ [p=~~~3b. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (sem [[1 1] " ;"])
        [p=[p=1 q=1] q=~]

---

###++ser 

```
++  ser  (just ']')                                     ::  Square Right
```

Parse ASCII character 93, ser.

####Examples

        ~tadbyl-hilbel/try=> (scan "]" ser)
        ~~~5d.
        ~tadbyl-hilbel/try=> `cord`(scan "]" ser)
        ']'
        ~tadbyl-hilbel/try=> (ser [[1 1] "]"])
        [p=[p=1 q=2] q=[~ [p=~~~5d. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (ser [[1 1] "[ ]"])
        [p=[p=1 q=1] q=~]

---

###++sig 

```
++  sig  (just '~')                                     ::  SIGnature squiggle
```

Parse ASCII character 126, sig.

####Examples

        ~tadbyl-hilbel/try=> (scan "~" sig)
        ~~~~
        ~tadbyl-hilbel/try=> `cord`(scan "~" sig)
        '~'
        ~tadbyl-hilbel/try=> (sig [[1 1] "~"])
        [p=[p=1 q=2] q=[~ [p=~~~~ q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (sig [[1 1] "?~"])
        [p=[p=1 q=1] q=~]

---

###++soq 

```
++  soq  (just '\'')                                    ::  Single Quote
```

Parse ASCII character 39, soq.
Note the extra '\' in the slam of soq with just is to escape the first soq because soq denotes a crip.

####Examples

        ~tadbyl-hilbel/try=> (scan "'" soq)
        ~~~27.
        ~tadbyl-hilbel/try=> `cord`(scan "'" soq)
        '''
        ~tadbyl-hilbel/try=> (soq [[1 1] "'"])
        [p=[p=1 q=2] q=[~ [p=~~~27. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (soq [[1 1] ">'"])
        [p=[p=1 q=1] q=~]

---

###++tar 

```
++  tar  (just '*')                                     ::  sTAR
```

Parse ASCII character 42, tar.

####Examples

        ~tadbyl-hilbel/try=> (scan "*" tar)
        ~~~2a.
        ~tadbyl-hilbel/try=> `cord`(scan "*" tar)
        '*'
        ~tadbyl-hilbel/try=> (tar [[1 1] "*"])
        [p=[p=1 q=2] q=[~ [p=~~~2a. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (tar [[1 1] ".*"])
        [p=[p=1 q=1] q=~]

---

###++tec 

```
++  tec  (just '`')                                     ::  backTiCk
```

Parse ASCII character 96, tec.

####Examples

        ~tadbyl-hilbel/try=> (scan "`" tec)
        ~~~6.
        ~tadbyl-hilbel/try=> `cord`(scan "`" tec)
        '`'
        ~tadbyl-hilbel/try=> (tec [[1 1] "`"])
        [p=[p=1 q=2] q=[~ [p=~~~6. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (tec [[1 1] " `"])
        [p=[p=1 q=1] q=~]

---

###++tis 

```
++  tis  (just '=')                                     ::  'tis tis, it is
```

Parse ASCII character 61, tis.

####Examples

        ~tadbyl-hilbel/try=> (scan "=" tis)
        ~~~3d.
        ~tadbyl-hilbel/try=> `cord`(scan "=" tis)
        '='
        ~tadbyl-hilbel/try=> (tis [[1 1] "="])
        [p=[p=1 q=2] q=[~ [p=~~~3d. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (tis [[1 1] "|="])
        [p=[p=1 q=1] q=~]
---

###++wut 

```
++  wut  (just '?')                                     ::  wut, what?
```

Parse ASCII character 63, wut.

###Examples

        ~tadbyl-hilbel/try=> (scan "?" wut)
        ~~~3f.
        ~tadbyl-hilbel/try=> `cord`(scan "?" wut)
        '?'
        ~tadbyl-hilbel/try=> (wut [[1 1] "?"])
        [p=[p=1 q=2] q=[~ [p=~~~3f. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (wut [[1 1] ".?"])
        [p=[p=1 q=1] q=~]

---

###++zap 

```
++  zap  (just '!')                                     ::  zap! bang! crash!!
```

Parse ASCII character 33, zap.

###Examples

        ~tadbyl-hilbel/try=> (scan "!" zap)
        ~~~21.
        ~tadbyl-hilbel/try=> `cord`(scan "!" zap)
        '!'
        ~tadbyl-hilbel/try=> (zap [[1 1] "!"])
        [p=[p=1 q=2] q=[~ [p=~~~21. q=[p=[p=1 q=2] q=""]]]]
        ~tadbyl-hilbel/try=> (zap [[1 1] "?!"])
        [p=[p=1 q=1] q=~]

---


