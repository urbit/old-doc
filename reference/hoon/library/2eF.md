section 2eF, parsing (ascii)          

---

###++ace

```
++  ace  (just ' ')                                     ::  spACE
```

Parse ASCII character 32, ace.

###Examples

        ~zod/try=> (scan " " ace)
        ~~. 
        ~zod/try=> `cord`(scan " " ace)
        ' '
        ~zod/try=> (ace [[1 1] " "])
        [p=[p=1 q=2] q=[~ [p=~~. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (ace [[1 1] " abc "])
        [p=[p=1 q=2] q=[~ [p=~~. q=[p=[p=1 q=2] q="abc "]]]]

---

###++bar 

```
++  bar  (just '|')                                     ::  vertical BAR
```

Parse ASCII character 124, bar.

####Examples

       ~zod/try=> (scan "|" bar)
        ~~~7c. 
        ~zod/try=> `cord`(scan "|" bar)
        '|'
        ~zod/try=> (bar [[1 1] "|"])
        [p=[p=1 q=2] q=[~ [p=~~~7c. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (bar [[1 1] "|="])
        [p=[p=1 q=2] q=[~ [p=~~~7c. q=[p=[p=1 q=2] q="="]]]]

---

###++bas 

```
++  bas  (just '\\')                                    ::  Back Slash (escaped)
```

Parse ASCII character 92, bas.
Note the extra '\' in the slam of bas with just is to escape the escape character, bas.

###Examples

        ~zod/try=> (scan "\\" bas)
        ~~~5c.
        ~zod/try=> `cord`(scan "\\" bas)
        '\'
        ~zod/try=> (bas [[1 1] "\"])
        ~ <syntax error at [1 18]>
        ~zod/try=> (bas [[1 1] "\\"])
        [p=[p=1 q=2] q=[~ [p=~~~5c. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (bas [[1 1] "\""])
        [p=[p=1 q=1] q=~]

---

###++buc 

```
++  buc  (just '$')                                     ::  dollars BUCks
```

Parse ASCII character 36, buc.

####Examples

        ~zod/try=> (scan "$" buc)
        ~~~24.
        ~zod/try=> `cord`(scan "$" buc)
        '$'
        ~zod/try=> (buc [[1 1] "$"])
        [p=[p=1 q=2] q=[~ [p=~~~24. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (buc [[1 1] "$%"])
        [p=[p=1 q=2] q=[~ [p=~~~24. q=[p=[p=1 q=2] q="%"]]]]

---

###++cab 

```
++  cab  (just '_')                                     ::  CABoose
```

Parse ASCII character 95, cab.

###Examples

        ~zod/try=> (scan "_" cab)
        ~~~5f.
        ~zod/try=> `cord`(scan "_" cab)
        '_'
        ~zod/try=> (cab [[1 1] "_"])
        [p=[p=1 q=2] q=[~ [p=~~~5f. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (cab [[1 1] "|_"])
        [p=[p=1 q=1] q=~]

---

###++cen 

```
++  cen  (just '%')                                     ::  perCENt
```

Parse ASCII character 37, cen.

####Examples

        ~zod/try=> (scan "%" cen)
        ~~~25.
        ~zod/try=> `cord`(scan "%" cen)
        '%'
        ~zod/try=> (cen [[1 1] "%"])
        [p=[p=1 q=2] q=[~ [p=~~~25. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (cen [[1 1] "%^"])
        [p=[p=1 q=2] q=[~ [p=~~~25. q=[p=[p=1 q=2] q="^"]]]] 

---

###++col 

```
++  col  (just ':')                                     ::  COLon
```

Parse ASCII character 58, col.

###Examples

        ~zod/try=> (scan ":" col)
        ~~~3a.
        ~zod/try=> `cord`(scan ":" col)
        ':'
        ~zod/try=> (col [[1 1] ":"])
        [p=[p=1 q=2] q=[~ [p=~~~3a. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (col [[1 1] ":-"])
        [p=[p=1 q=2] q=[~ [p=~~~3a. q=[p=[p=1 q=2] q="-"]]]]

---

###++com 

```
++  com  (just ',')                                     ::  COMma
```

Parse ASCII character 44, com.

####Examples

        ~zod/try=> (scan "," com)
        ~~~2c.
        ~zod/try=> `cord`(scan "," com)
        ','
        ~zod/try=> (com [[1 1] ","])
        [p=[p=1 q=2] q=[~ [p=~~~2c. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (com [[1 1] "not com"])
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

        ~zod/try=> (scan "." dot)
        ~~~.
        ~zod/try=> `cord`(scan "." dot)
        '.'
        ~zod/try=> (dot [[1 1] "."])
        [p=[p=1 q=2] q=[~ [p=~~~. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (dot [[1 1] ".^"])
        [p=[p=1 q=2] q=[~ [p=~~~. q=[p=[p=1 q=2] q="^"]]]]

---

###++fas 

```
++  fas  (just '/')                                     ::  Forward Slash
```

Parse ASCII character 47, fas.

###Examples

        ~zod/try=> (scan "/" fas)
        ~~~2f.
        ~zod/try=> `cord`(scan "/" fas)
        '/'
        ~zod/try=> (fas [[1 1] "/"])
        [p=[p=1 q=2] q=[~ [p=~~~2f. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (fas [[1 1] "|/"])
        [p=[p=1 q=1] q=~]

---

###++gal 

```
++  gal  (just '<')                                     ::  Greater Left
```

Parse ASCII character 60, gal.

####Examples

        ~zod/try=> (scan "<" gal)
        ~~~3c.
        ~zod/try=> `cord`(scan "<" gal)
        '<'
        ~zod/try=> (gal [[1 1] "<"])
        [p=[p=1 q=2] q=[~ [p=~~~3c. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (gal [[1 1] "<+"])
        [p=[p=1 q=2] q=[~ [p=~~~3c. q=[p=[p=1 q=2] q="+"]]]]
        ~zod/try=> (gal [[1 1] "+<"])
        [p=[p=1 q=1] q=~]

---

###++gar 

```
++  gar  (just '>')                                     ::  Greater Right
```

Parse ASCII character 62, gar.

####Examples

        ~zod/try=> (scan ">" gar)
        ~~~3e.
        ~zod/try=> `cord`(scan ">" gar)
        '>'
        ~zod/try=> (gar [[1 1] ">"])
        [p=[p=1 q=2] q=[~ [p=~~~3e. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (gar [[1 1] "=>"])
        [p=[p=1 q=1] q=~]

---

###++hax 

```
++  hax  (just '#')                                     ::  Hash
```

Parse ASCII character 35, hax.

####Examples

        ~zod/try=> (scan "#" hax)
        ~~~23.
        ~zod/try=> `cord`(scan "#" hax)
        '#'
        ~zod/try=> (hax [[1 1] "#"])
        [p=[p=1 q=2] q=[~ [p=~~~23. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (hax [[1 1] "#!"])
        [p=[p=1 q=2] q=[~ [p=~~~23. q=[p=[p=1 q=2] q="!"]]]]

---

###++kel 

```
++  kel  (just '{')                                     ::  Curly Left
```

Parse ASCII character 123, kel.
Note that this, with ker, opens and closes a Hoon expression for Hoon string interpolation.  Escape kel to parse it.

####Examples

        ~zod/try=> (scan "\{" kel)
        ~~~7b.
        ~zod/try=> `cord`(scan "\{" kel)
        '{'
        ~zod/try=> (kel [[1 1] "\{"])
        [p=[p=1 q=2] q=[~ [p=~~~7b. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (kel [[1 1] " \{"])
        [p=[p=1 q=1] q=~]

---

###++ker 

```
++  ker  (just '}')                                     ::  Curly Right
```

Parse ASCII character 125, ker.

###Examples

        ~zod/try=> (scan "}" ker)
        ~~~7d.
        ~zod/try=> `cord`(scan "}" ker)
        '}'
        ~zod/try=> (ker [[1 1] "}"])
        [p=[p=1 q=2] q=[~ [p=~~~7d. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (ker [[1 1] "\{}"])
        [p=[p=1 q=1] q=~]

---

###++ket 

```
++  ket  (just '^')                                     ::  CareT
```

Parse ASCII character 94, ket.

####Examples

        ~zod/try=> (scan "^" ket)
        ~~~5e.
        ~zod/try=> `cord`(scan "^" ket)
        '^'
        ~zod/try=> (ket [[1 1] "^"])
        [p=[p=1 q=2] q=[~ [p=~~~5e. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (ket [[1 1] ".^"])
        [p=[p=1 q=1] q=~]

---

###++lus 

```
++  lus  (just '+')                                     ::  pLUS
```

Parse ASCII character 43, lus.

###Examples

        ~zod/try=> (scan "+" lus)
        ~~~2b.
        ~zod/try=> `cord`(scan "+" lus)
        '+'
        ~zod/try=> (lus [[1 1] "+"])
        [p=[p=1 q=2] q=[~ [p=~~~2b. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (lus [[1 1] ".+"])
        [p=[p=1 q=1] q=~]

---

###++hep 

```
++  hep  (just '-')                                     ::  HyPhen
```

Parse ASCII character 45, hep.

####Examples

        ~zod/try=> (scan "-" hep)
        ~~-
        ~zod/try=> `cord`(scan "-" hep)
        '-'
        ~zod/try=> (hep [[1 1] "-"])
        [p=[p=1 q=2] q=[~ [p=~~- q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (hep [[1 1] ":-"])
        [p=[p=1 q=1] q=~]

---

###++pel 

```
++  pel  (just '(')                                     ::  Paren Left
```

Parse ASCII character 40, pel.

####Examples

        ~zod/try=> (scan "(" pel)
        ~~~28.
        ~zod/try=> `cord`(scan "(" pel)
        '('
        ~zod/try=> (pel [[1 1] "("])
        [p=[p=1 q=2] q=[~ [p=~~~28. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (pel [[1 1] ";("])
        [p=[p=1 q=1] q=~]

---

###++pam 

```
++  pam  (just '&')                                     ::  AMPersand pampersand
```

Parse ASCII character 38, pam.

####Examples

        ~zod/try=> (scan "&" pam)
        ~~~26.
        ~zod/try=> `cord`(scan "&" pam)
        '&'
        ~zod/try=> (pam [[1 1] "&"])
        [p=[p=1 q=2] q=[~ [p=~~~26. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (pam [[1 1] "?&"])
        [p=[p=1 q=1] q=~]

---

###++per 

```
++  per  (just ')')                                     ::  Paren Right
```

Parse ASCII character 41, per.

###Examples

        ~zod/try=> (scan ")" per)
        ~~~29.
        ~zod/try=> `cord`(scan ")" per)
        ')'
        ~zod/try=> (per [[1 1] ")"])
        [p=[p=1 q=2] q=[~ [p=~~~29. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (per [[1 1] " )"])
        [p=[p=1 q=1] q=~]

---

###++pat 

```
++  pat  (just '@')                                     ::  AT pat
```

Parse ASCII character 64, pat.

####Examples

        ~zod/try=> (scan "@" pat)
        ~~~4.
        ~zod/try=> `cord`(scan "@" pat)
        '@'
        ~zod/try=> (pat [[1 1] "@"])
        [p=[p=1 q=2] q=[~ [p=~~~4. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (pat [[1 1] "?@"])
        [p=[p=1 q=1] q=~]

---

###++sel

```
++  sel  (just '[')                                     ::  Square Left
```

Parse ASCII character 91, sel.

####Examples

        ~zod/try=> (scan "[" sel)
        ~~~5b.
        ~zod/try=> `cord`(scan "[" sel)
        '['
        ~zod/try=> (sel [[1 1] "["])
        [p=[p=1 q=2] q=[~ [p=~~~5b. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (sel [[1 1] "-["])
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

        ~zod/try=> (scan "]" ser)
        ~~~5d.
        ~zod/try=> `cord`(scan "]" ser)
        ']'
        ~zod/try=> (ser [[1 1] "]"])
        [p=[p=1 q=2] q=[~ [p=~~~5d. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (ser [[1 1] "[ ]"])
        [p=[p=1 q=1] q=~]

---

###++sig 

```
++  sig  (just '~')                                     ::  SIGnature squiggle
```

Parse ASCII character 126, sig.

####Examples

        ~zod/try=> (scan "~" sig)
        ~~~~
        ~zod/try=> `cord`(scan "~" sig)
        '~'
        ~zod/try=> (sig [[1 1] "~"])
        [p=[p=1 q=2] q=[~ [p=~~~~ q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (sig [[1 1] "?~"])
        [p=[p=1 q=1] q=~]

---

###++soq 

```
++  soq  (just '\'')                                    ::  Single Quote
```

Parse ASCII character 39, soq.
Note the extra '\' in the slam of soq with just is to escape the first soq because soq denotes a crip.

####Examples

        ~zod/try=> (scan "'" soq)
        ~~~27.
        ~zod/try=> `cord`(scan "'" soq)
        '''
        ~zod/try=> (soq [[1 1] "'"])
        [p=[p=1 q=2] q=[~ [p=~~~27. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (soq [[1 1] ">'"])
        [p=[p=1 q=1] q=~]

---

###++tar 

```
++  tar  (just '*')                                     ::  sTAR
```

Parse ASCII character 42, tar.

####Examples

        ~zod/try=> (scan "*" tar)
        ~~~2a.
        ~zod/try=> `cord`(scan "*" tar)
        '*'
        ~zod/try=> (tar [[1 1] "*"])
        [p=[p=1 q=2] q=[~ [p=~~~2a. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (tar [[1 1] ".*"])
        [p=[p=1 q=1] q=~]

---

###++tec 

```
++  tec  (just '`')                                     ::  backTiCk
```

Parse ASCII character 96, tec.

####Examples

        ~zod/try=> (scan "`" tec)
        ~~~6.
        ~zod/try=> `cord`(scan "`" tec)
        '`'
        ~zod/try=> (tec [[1 1] "`"])
        [p=[p=1 q=2] q=[~ [p=~~~6. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (tec [[1 1] " `"])
        [p=[p=1 q=1] q=~]

---

###++tis 

```
++  tis  (just '=')                                     ::  'tis tis, it is
```

Parse ASCII character 61, tis.

####Examples

        ~zod/try=> (scan "=" tis)
        ~~~3d.
        ~zod/try=> `cord`(scan "=" tis)
        '='
        ~zod/try=> (tis [[1 1] "="])
        [p=[p=1 q=2] q=[~ [p=~~~3d. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (tis [[1 1] "|="])
        [p=[p=1 q=1] q=~]
---

###++wut 

```
++  wut  (just '?')                                     ::  wut, what?
```

Parse ASCII character 63, wut.

###Examples

        ~zod/try=> (scan "?" wut)
        ~~~3f.
        ~zod/try=> `cord`(scan "?" wut)
        '?'
        ~zod/try=> (wut [[1 1] "?"])
        [p=[p=1 q=2] q=[~ [p=~~~3f. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (wut [[1 1] ".?"])
        [p=[p=1 q=1] q=~]

---

###++zap 

```
++  zap  (just '!')                                     ::  zap! bang! crash!!
```

Parse ASCII character 33, zap.

###Examples

        ~zod/try=> (scan "!" zap)
        ~~~21.
        ~zod/try=> `cord`(scan "!" zap)
        '!'
        ~zod/try=> (zap [[1 1] "!"])
        [p=[p=1 q=2] q=[~ [p=~~~21. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (zap [[1 1] "?!"])
        [p=[p=1 q=1] q=~]

---


