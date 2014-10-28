##section 2eF, parsing (ascii)          

###++ace

Space

```
++  ace  (just ' ')
```

Parses ASCII character 32, space.

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

Vertical bar

```
++  bar  (just '|')
```

Parses ASCII character 124, the vertical bar.

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

Backslash

```
++  bas  (just '\\')
```

Parses ASCII character 92, the backslash.
Note the extra '\' in the slam of bas with just is to escape the escape character, bas.

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

Dollar sign

```
++  buc  (just '$')
```

Parses ASCII character 36, the dollar sign.

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

Underscore

```
++  cab  (just '_')
```

Parses ASCII character 95, the underscore.

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

Percent sign

```
++  cen  (just '%')
```

Parses ASCII character 37, the percent sign.

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

Colon

```
++  col  (just ':')
```

Parses ASCII character 58, the colon

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

Comma

```
++  com  (just ',')
```

Parses ASCII character 44, the comma.

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

Double quote

```
++  doq  (just '"')
```

Parses ASCII character 34, doq.

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

Period

```
++  dot  (just '.')
```

Parses ASCII character 46, the period.

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

Forward slash

```
++  fas  (just '/')
```

Parses ASCII character 47, the forward slash.

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

Less-than sign

```
++  gal  (just '<')
```

Parses ASCII character 60, the less-than sign.

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

Greater-than sign

```
++  gar  (just '>')
```

Parses ASCII character 62, the greater-than sign.

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

Number sign

```
++  hax  (just '#')
```

Parses ASCII character 35, the number sign.

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

Left curley bracket

```
++  kel  (just '{')
```

Parses ASCII character 123, the left cutly bracket.
Note that `kel` and `ker` open and close a Hoon expression for Hoon string interpolation.To parse either of them, they must be escaped.

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

Right curley bracket

```
++  ker  (just '}')
```

Parses ASCII character 125, ker.

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

Caret

```
++  ket  (just '^')
```

Parses ASCII character 94, the caret.

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
++  lus  (just '+')
```

Parses ASCII character 43, the plus sign.

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
++  hep  (just '-')
```

Parses ASCII character 45, the hyphen.

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

Left parenthesis

```
++  pel  (just '(')
```

Parses ASCII character 40, the left parenthesis.

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

Ampersand

```
++  pam  (just '&')
```

Parses ASCII character 38, the ampersand.

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

Right parenthesis

```
++  per  (just ')')
```

Parses ASCII character 41, the right parenthesis.

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

"At" sign

```
++  pat  (just '@')
```

Parses ASCII character 64, the "at" sign.

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

Left square bracket

```
++  sel  (just '[')
```

Parses ASCII character 91, the left square bracket.

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

Semicolon

```
++  sem  (just ';')
```

Parses ASCII character 59, the semicolon.

###Examples

    ~zod/try=> (scan ";" sem)
    ~~~3b.
    ~zod/try=> `cord`(scan ";" sem)
    ';'
    ~zod/try=> (sem [[1 1] ";"])
    [p=[p=1 q=2] q=[~ [p=~~~3b. q=[p=[p=1 q=2] q=""]]]]
    ~zod/try=> (sem [[1 1] " ;"])
    [p=[p=1 q=1] q=~]

---

###++ser 

Right square bracket

```
++  ser  (just ']')
```

Parses ASCII character 93, the right square bracket.

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

Tilde

```
++  sig  (just '~')
```

Parses ASCII character 126, the tilde.

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

Single quote

```
++  soq  (just '\'')
```

Parses ASCII character 39, soq.
Note the extra '\' is to escape the first `soq` because soq denotes a crip.

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

Asterisk

```
++  tar  (just '*')
```

Parses ASCII character 42, the asterisk.

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

Backtick

```
++  tec  (just '`')                                     ::  backTiCk
```

Parses ASCII character 96, the backtick (also known as the "grave accent".

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

Equals sign

```
++  tis  (just '=')
```

Parses ASCII character 61, the equals sign.

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

Question mark

```
++  wut  (just '?')
```

Parses ASCII character 63, wut.

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

Exclamation point

```
++  zap  (just '!')
```

Parses ASCII character 33, the exclamation point zap.

        ~zod/try=> (scan "!" zap)
        ~~~21.
        ~zod/try=> `cord`(scan "!" zap)
        '!'
        ~zod/try=> (zap [[1 1] "!"])
        [p=[p=1 q=2] q=[~ [p=~~~21. q=[p=[p=1 q=2] q=""]]]]
        ~zod/try=> (zap [[1 1] "?!"])
        [p=[p=1 q=1] q=~]

---
