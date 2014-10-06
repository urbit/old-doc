##section 2dA, sets

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
 
    ~zod/try=> =b (sa `(list ,@t)`['john' 'bonita' 'daniel' 'madeleine' ~])
    ~zod/try=> (apt b)
        %.y
    ~zod/try=> =m (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ['c' 4] ['d' 5] ~])
    ~zod/try=> m
        {[p='d' q=5] [p='a' q=1] [p='c' q=4] [p='b' q=[2 3]]}
    ~zod/try=> (apt m)
        %.y

---

###++in


```
++  in                                                  ::  set engine
  ~/  %in
  |/  a=(set)
```

Set manipulation arms

    ~zod/try=> ~(. in (sa "asd"))
    <13.evb [nlr(^$1{@tD $1}) <414.fvk 101.jzo 1.ypj %164>]>

###+-all:in


```
  +-  all                                               ::  logical AND
    ~/  %all
    |*  b=$+(* ?)
    |-  ^-  ?
    ?~  a
      &
    ?&((b n.a) $(a l.a) $(a r.a))
  ::
```

Every member in the set matches a predicate.

    ~zod/try=> =b (sa `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
    ~zod/try=> (~(all in b) |=(a=* ?@(+.a & |)))
        %.n
    ~zod/try=> =b (sa `(list ,@t)`['john' 'bonita' 'daniel' 'madeleine' ~])
    ~zod/try=> (~(all in b) |=(a=@t (gte a 100)))
        %.y

---

###+-any:in


```
  +-  any                                               ::  logical OR
    ~/  %any
    |*  b=$+(* ?)
    |-  ^-  ?
    ?~  a
      |
    ?|((b n.a) $(a l.a) $(a r.a))
  ::
```

A member in the set matches a predicate.

    ~zod/try=> =b (sa `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
    ~zod/try=> (~(any in b) |=(a=* ?@(+.a & |)))
        %.y
    ~zod/try=> =b (sa `(list ,@t)`['john' 'bonita' 'daniel' 'madeleine' ~])
    ~zod/try=> (~(any in b) |=(a=@t (lte a 100)))
        %.n

---

###+-del:in


```
  +-  del                                               ::  b without any a
    ~/  %del
    |*  b=*
    |-  ^+  a
    ?~  a
      ~
    ?.  =(b n.a)
      ?:  (hor b n.a)
        [n.a $(a l.a) r.a]
      [n.a l.a $(a r.a)]
    |-  ^-  ?(~ _a)
    ?~  l.a  r.a
    ?~  r.a  l.a
    ?:  (vor n.l.a n.r.a)
      [n.l.a l.l.a $(l.a r.l.a)]
    [n.r.a $(r.a l.r.a) r.r.a]
  ::
```

Accept a noun and removes it from the set.

    ~zod/try=> =b (sa `(list ,@t)`['a' 'b' 'c' ~])
    ~zod/try=> (~(del in b) 'a')
    {'c' 'b'}
    ~zod/try=> =b (sa `(list ,@t)`['john' 'bonita' 'daniel' 'madeleine' ~])
    ~zod/try=> (~(del in b) 'john')
    {'bonita' 'madeleine' 'daniel'}
    ~zod/try=> (~(del in b) 'susan')
    {'bonita' 'madeleine' 'daniel' 'john'}

---

###+-dig:in


```
  +-  dig                                               ::  axis of a in b
    |=  b=*
    =+  c=1
    |-  ^-  (unit ,@)
    ?~  a  ~
    ?:  =(b n.a)  [~ u=(peg c 2)]
    ?:  (gor b n.a)
      $(a l.a, c (peg c 6))
    $(a r.a, c (peg c 7))
  ::
```

Produce the axis of a noun within the set.

    ~zod/try=> =a (sa `(list ,@)`[1 2 3 4 5 6 7 ~])
    ~zod/try=> a
    {5 4 7 6 1 3 2}
    ~zod/try=> -.a
    n=6
    ~zod/try=> (~(dig in a) 7)
    [~ 12]
    ~zod/try=> (~(dig in a) 2)
    [~ 14]
    ~zod/try=> (~(dig in a) 6)
    [~ 2]

---

###+-gas:in


```
  +-  gas                                               ::  concatenate
    ~/  %gas
    |=  b=(list ,_?>(?=(^ a) n.a))
    |-  ^+  a
    ?~  b
      a
    $(b t.b, a (put(+< a) i.b))
  ::
```

Insert the elements of a list into the set.

    ~zod/try=> b
    {'bonita' 'madeleine' 'rudolf' 'john'}
    ~zod/try=> (~(gas in b) `(list ,@t)`['14' 'things' 'number' '1.337' ~])
    {'1.337' '14' 'number' 'things' 'bonita' 'madeleine' 'rudolf' 'john'}
    ~zod/try=> (~(gas in s) `(list ,@t)`['1' '2' '3' ~])
    {'1' '3' '2' 'e' 'd' 'a' 'c' 'b'}

---

###+-has:in


```
  +-  has                                               ::  b exists in a check
    ~/  %has
    |*  b=*
    |-  ^-  ?
    ?~  a
      |
    ?:  =(b n.a)
      &
    ?:  (hor b n.a)
      $(a l.a)
    $(a r.a)
  ::
```

Whether the set contains an element.

    ~zod/try=> =a (~(gas in `(set ,@t)`~) `(list ,@t)`[`a` `b` `c` ~])
    ~zod/try=> (~(has in a) `a`)
    %.y
    ~zod/try=> (~(has in a) 'z')
    %.n

---

###+-put:in


```
  +-  put                                               ::  puts b in a, sorted
    ~/  %put
    |*  b=*
    |-  ^+  a
    ?~  a
      [b ~ ~]
    ?:  =(b n.a)
      a
    ?:  (hor b n.a)
      =+  c=$(a l.a)
      ?>  ?=(^ c)
      ?:  (vor n.a n.c)
        [n.a c r.a]
      [n.c l.c [n.a r.c r.a]]
    =+  c=$(a r.a)
    ?>  ?=(^ c)
    ?:  (vor n.a n.c)
      [n.a l.a c]
    [n.c [n.a l.a l.c] r.c]
  ::
```

Add an element to the set.

    ~zod/try=> =a (~(gas in `(set ,@t)`~) `(list ,@t)`[`a` `b` `c` ~])
    ~zod/try=> =b (~(put in a) `d`)
    ~zod/try=> b
    {`d` `a` `c` `b`}
    ~zod/try=> -.l.+.b
    n=`d`

---

###+-rep:in


```
  +-  rep                                               ::  replace by tile
    |*  [b=* c=_,*]
    |-
    ?~  a  b
    $(a r.a, b $(a l.a, b (c n.a b)))
  ::
```

Accumulate value from elements of set.

XX interface changing

    ~zod/try=> =a (~(gas in *(set ,@)) [1 2 3 ~])
    ~zod/try=> a
    {1 3 2}
    ~zod/try=> (~(rep in a) 0 |=([a=@ b=@] (add a b)))
    6

---

###+-tap:in


```
  +-  tap                                               ::  list tiles a set
    ~/  %tap
    |=  b=(list ,_?>(?=(^ a) n.a))
    ^+  b
    ?~  a
      b
    $(a r.a, b [n.a $(a l.a)])
  ::
```

Flatten the set into a list.

    ~zod/try=> =s (sa `(list ,@t)`['a' 'b' 'c' 'd' 'e' ~])
    ~zod/try=> s
    {'e' 'd' 'a' 'c' 'b'}
    ~zod/try=> (~(tap in s) `(list ,@t)`['1' '2' '3' ~])
    ~['b' 'c' 'a' 'd' 'e' '1' '2' '3']
    ~zod/try=> b
    {'bonita' 'madeleine' 'daniel' 'john'}
    ~zod/try=> (~(tap in b) `(list ,@t)`['david' 'people' ~])
    ~['john' 'daniel' 'madeleine' 'bonita' 'david' 'people']

---

###+-wyt:in


```
  +-  wyt                                               ::  size of set
    .+
    |-  ^-  @
    ?~(a 0 +((add $(a l.a) $(a r.a))))
```

Produce the cardinality (number of elements) of the set.

    ~zod/try=> =a (~(gas in `(set ,@t)`~) `(list ,@t)`[`a` `b` `c` ~])
    ~zod/try=> ~(wyt in a)
    4
    ~zod/try=> b
    {'bonita' 'madeleine' 'daniel' 'john'}
    ~zod/try=> ~(wyt in b)
    5

---
