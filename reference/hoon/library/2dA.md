section 2dA, sets     
---
                
###++apt

```
++  apt                                                 ::  set invariant
  |=  a=(tree)
  ?~  a
    &
  ?&  ?~(l.a & ?&((vor n.a n.l.a) (hor n.l.a n.a)))
      ?~(r.a & ?&((vor n.a n.r.a) (hor n.a n.r.a)))
  ==
::
```

Accept any tree and produce a loobean indicating whether the tree is a set.

####Examples 

        ~tadbyl-hilbel/try=> =b (sa `(list ,@t)`['john' 'bonita' 'daniel' 'madeleine' ~])
        ~tadbyl-hilbel/try=> (apt b)
        %.y
        ---
        ~tadbyl-hilbel/try=> =m (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ['c' 4] ['d' 5] ~])
        ~tadbyl-hilbel/try=> m
        {[p='d' q=5] [p='a' q=1] [p='c' q=4] [p='b' q=[2 3]]}
        ~tadbyl-hilbel/try=> (apt m)
        %.y

---

###++in

```
++  in                                                  ::  set engine
  ~/  %in
  |/  a=(set)
```


##+-  all

Accept a gate which accepts any noun and produce a loobean.  Slam the gate with each member
of set 'a', produce the logical AND of the transformed set.

####Examples

        ~dovryp-toblug/try=> =b (sa `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
        ~dovryp-toblug/try=> (~(all in b) |=(a=* ?@(-.a & |)))
        %.n
        ~tadbyl-hilbel/try=> =b (sa `(list ,@t)`['john' 'bonita' 'daniel' 'madeleine' ~])
        ~tadbyl-hilbel/try=> (~(all in b) |=(a=@t (gte a 100)))
        %.y

---

##+-  any

Accept a gate which accepts any noun and produce a loobean.  Slam the gate with each member
of set 'a', produce the logical OR of the transformed set.

####Examples:

        ~dovryp-toblug/try=> =b (sa `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
        ~dovryp-toblug/try=> (~(any in b) |=(a=* ?@(+.a & |)))
        %.y
        ~tadbyl-hilbel/try=> =b (sa `(list ,@t)`['john' 'bonita' 'daniel' 'madeleine' ~])
        ~tadbyl-hilbel/try=> (~(any in b) |=(a=@t (lte a 100)))
        %.n

---

##+-  del

Accept any noun 'b' and removes it from the set 'a'.

####Examples

        ~dovryp-toblug/try=> =b (sa `(list ,@t)`[`a` `b` `c` ~])
        ~dovryp-toblug/try=> (~(del in b) `a`)
        {`c` `b`}
        ---
        ~tadbyl-hilbel/try=> =b (sa `(list ,@t)`['john' 'bonita' 'daniel' 'madeleine' ~])
        ~tadbyl-hilbel/try=> (~(del in b) 'john')
        {'bonita' 'madeleine' 'daniel'}
        ---
        ~tadbyl-hilbel/try=> (~(del in b) 'susan')
        {'bonita' 'madeleine' 'daniel' 'john'}

---

##+-  dig

Produce the axis of the noun `b` within the set `a`.

####Examples

        ~talsur-todres/try=> =a (sa `(list ,@)`[1 2 3 4 5 6 7 ~])
        ~talsur-todres/try=> a
        {5 4 7 6 1 3 2}
        ~talsur-todres/try=> -.a
        n=6
        ~talsur-todres/try=> (~(dig in a) 7)
        [~ 12]
        ~talsur-todres/try=> (~(dig in a) 2)
        [~ 14]
        ~talsur-todres/try=> (~(dig in a) 6)
        [~ 2]

---

##+-  gas

Accept a list 'b' with members of the same type as the set 'a' and produce
the union set of 'a' and 'b'.

####Examples

        ~tadbyl-hilbel/try=> b
        {'bonita' 'madeleine' 'rudolf' 'john'}
        ~tadbyl-hilbel/try=> (~(gas in b) `(list ,@t)`['14' 'things' 'number' '1.337' ~])
        {'1.337' '14' 'number' 'things' 'bonita' 'madeleine' 'rudolf' 'john'}
        ---
        ~tadbyl-hilbel/try=> (~(gas in s) `(list ,@t)`['1' '2' '3' ~])
        {'1' '3' '2' 'e' 'd' 'a' 'c' 'b'}

---

##+-  has

Accepts any noun and produces the loobean indicating whether or not that value (n.a) exists in 'a'.

####Examples

        ~dovryp-toblug/try=> =a (~(gas in `(set ,@t)`~) `(list ,@t)`[`a` `b` `c` ~])
        ~dovryp-toblug/try=> (~(has in a) `a`)
        %.y
        ~dovryp-toblug/try=> (~(has in a) 'z')
        %.n

---

##+-  put

Accept any noun 'b' and produce the set 'a' with 'b' added to its sorted location.

####Examples

        ~talsur-todres/try=> =a (~(gas in `(set ,@t)`~) `(list ,@t)`[`a` `b` `c` ~])
        ~talsur-todres/try=> =b (~(put in a) `d`)
        ~talsur-todres/try=> b
        {`d` `a` `c` `b`}
        ~talsur-todres/try=> -.l.+.b
        n=`d`

---

##+-  rep

Accept a noun and a binary gate.  Produce the 'a' with each member 'n.a' replaced by (c n.a b).

####Examples

        ~talsur-todres/try=> =a (~(gas in *(set ,@)) [1 2 3 ~])
        ~talsur-todres/try=> a
        {1 3 2}
        ~talsur-todres/try=> (~(rep in a) 0 |=([a=@ b=@] (add a b)))
        6

---

##+-  tap

Accept a list of elements of the set and produce a cell of the set with the list concatenated.

####Examples

        ~tadbyl-hilbel/try=> =s (sa `(list ,@t)`['a' 'b' 'c' 'd' 'e' ~])
        ~tadbyl-hilbel/try=> s
        {'e' 'd' 'a' 'c' 'b'}
        ~tadbyl-hilbel/try=> (~(tap in s) `(list ,@t)`['1' '2' '3' ~])
        ~['b' 'c' 'a' 'd' 'e' '1' '2' '3']
        ~tadbyl-hilbel/try=> b
        {'bonita' 'madeleine' 'daniel' 'john'}
        ~tadbyl-hilbel/try=> (~(tap in b) `(list ,@t)`['david' 'people' ~])
        ~['john' 'daniel' 'madeleine' 'bonita' 'david' 'people']

---

##+-  wyt

Produce the cardinality (number of elements) of the set.

####Examples

        ~talsur-todres/try=> =a (~(gas in `(set ,@t)`~) `(list ,@t)`[`a` `b` `c` ~])
        ~talsur-todres/try=> ~(wyt in a)
        4
        ~tadbyl-hilbel/try=> b
        {'bonita' 'madeleine' 'daniel' 'john'}
        ~tadbyl-hilbel/try=> ~(wyt in b)
        5

---
