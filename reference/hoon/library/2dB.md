##section 2dB, maps

---

###++ept       


```
++  ept                                                 ::  map invariant
  |=  a=(tree ,[p=* q=*])
  ?~  a
    &
  ?&  ?~(l.a & ?&((vor p.n.a p.n.l.a) (hor p.n.l.a p.n.a)))
      ?~(r.a & ?&((vor p.n.a p.n.r.a) (hor p.n.a p.n.r.a)))
  ==
::
```


Is the given tree of cell pairs a map?

        ~zod/try=> m
        {[p='d' q=5] [p='a' q=1] [p='c' q=4] [p='b' q=[2 3]]}
        ~zod/try=> (ept m)
        %.y
        ~zod/try=> b
        {'bonita' 'madeleine' 'daniel' 'john'}
        ~zod/try=> (ept b)
        ! type-fail
        ! exit

---

###++ja


```
++  ja                                                  ::  jar engine
  |/  a=(jar)
```


The jar engine: A container arm for jar operation arms.  Jars are maps of lists.
The contained arms inherit the sample jar.

    ~zod/try=> ~(. ja (mo (limo a/"ho" b/"he" ~)))
    <2.dgz [nlr([p={%a %b} q=""]) <414.fvk 101.jzo 1.ypj %164>]>

---

###+-get:ja


```
  +-  get                                               ::  grab value by key
    |*  b=*
    =+  c=(~(get by a) b)
    ?~(c ~ u.c)
  ::
```

Retrieve a list from the map by its key.

    ~zod/try=> =l (mo `(list ,[@t (list ,@)])`[['a' `(list ,@)`[1 2 3 ~]] ['b' `(list ,@)`[4 5 6 ~]] ~])
    ~zod/try=> l
    {[p='a' q=~[1 2 3]] [p='b' q=~[4 5 6]]}
    ~zod/try=> (~(get ja l) 'a')
    ~[1 2 3]
    ~zod/try=> (~(get ja l) 'b')
    ~[4 5 6]
    ~zod/try=> (~(get ja l) 'c')
    ~

---

###+-add:ja


```
  +-  add                                               ::  adds key-list pair
    |*  [b=* c=*]
    =+  d=(get(+< a) b)
    (~(put by a) b [c d])
::
```

Add a key-list value to the jar.

    ~zod/try=> =l (mo `(list ,[@t (list ,@)])`[['a' `(list ,@)`[1 2 3 ~]] ['b' `(list ,@)`[4 5 6 ~]] ~])
    ~zod/try=> l
    {[p='a' q=~[1 2 3]] [p='b' q=~[4 5 6]]}
    ~zod/try=> (~(add ja l) 'b' 7)
    {[p='a' q=~[1 2 3]] [p='b' q=~[7 4 5 6]]}
    ~zod/try=> (~(add ja l) 'a' 100)
    {[p='a' q=~[100 1 2 3]] [p='b' q=~[4 5 6]]}
    ~zod/try=> (~(add ja l) 'c' 7)
    {[p='a' q=~[1 2 3]] [p='c' q=~[7]] [p='b' q=~[4 5 6]]}
    ~zod/try=> (~(add ja l) 'c' `(list ,@)`[7 8 9 ~])
    ! type-fail
    ! exit

---

###++ju


```
++  ju                                                  ::  jug engine
  |/  a=(jug)
```


The jug engine: container arm for jug operation arms.  Jugs are maps of sets.
The contained arms inherit it's sample jug, 'a'.

    ~zod/try=> ~(. ju (mo (limo a/(sa "ho") b/(sa "he") ~)))
    <2.dgz [nlr([p={%a %b} q={nlr(^$1{@tD $1}) nlr(^$3{@tD $3})}]) <414.fvk 101.jzo 1.ypj %164>]>

###+-del:ju


```
  +-  del                                               ::  delete at key b
    |*  [b=* c=*]
    ^+  a
    =+  d=(get(+< a) b)
    =+  e=(~(del in d) c)
    ?~  e
      (~(del by a) b)
    (~(put by a) b e)
  ::
```
        
Delete a value in a set at a key.

    ~zod/try=> s
    {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}
    ~zod/try=> (~(del ju s) 'a' 1)
    {[p='a' q={3 2}] [p='b' q={5 4 6}]}
    ~zod/try=> (~(del ju s) 'c' 7)
    {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}        

---

##+-get:ju

```
  +-  get                                               ::  gets set by key
    |*  b=*
    =+  c=(~(get by a) b)
    ?~(c ~ u.c)
  ::
```

Retrieve a set from the map by its key.

    ~zod/try=> s
    {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}
    ~zod/try=> (~(get ju s) 'a')
    {1 3 2}
    ~zod/try=> (~(get ju s) 'b')
    {5 4 6}
    ~zod/try=> (~(get ju s) 'c')
    ~
      
---

###+-has:ju


```
  +-  has                                               ::  existence check
    |*  [b=* c=*]
    ^-  ?
    (~(has in (get(+< a) b)) c)
  ::
```

Does a key have an elements in its set?

    ~zod/try=> s
    {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}
    ~zod/try=> (~(has ju s) 'a' 3)
    %.y
    ~zod/try=> (~(has ju s) 'b' 6)
    %.y
    ~zod/try=> (~(has ju s) 'a' 7)
    %.n
    ~zod/try=> (~(has jus s) 'c' 7)
    ! -find-limb.jus
    ! find-none
    ! exit
    ~zod/try=> (~(has ju s) 'c' 7)
    %.n

---

###+-put:ju


```
  +-  put                                               ::  adds key-element pair
    |*  [b=* c=*]
    ^+  a
    =+  d=(get(+< a) b)
    (~(put by a) b (~(put in d) c))
  ::
```

Add a value to a specific set in the jug.

    ~zod/try=> s
    {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}
    ~zod/try=> (~(put ju s) 'a' 7)
    {[p='a' q={7 1 3 2}] [p='b' q={5 4 6}]}
    ~zod/try=> (~(put ju s) 'a' 1)
    {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}
    ~zod/try=> (~(put ju s) 'c' 7)
    {[p='a' q={1 3 2}] [p='c' q={7}] [p='b' q={5 4 6}]}

---

###++by


```
++  by                                                  ::  map engine
  ~/  %by
  |/  a=(map)
```

Container arm for map operation arms.  The contained arms inherit it's sample map, 'a'. 

---

###+-all:by


```
  +-  all                                               ::  logical AND
    ~/  %all
    |*  b=$+(* ?)
    |-  ^-  ?
    ?~  a
      &
    ?&((b q.n.a) $(a l.a) $(a r.a))
  ::
```

Every value in the map matches a predicate.

    ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
    ~zod/try=> (~(all by b) |=(a=* ?@(a & |)))
    %.n
    ~zod/try=> =a (mo `(list ,[@t @u])`[['a' 1] ['b' 2] ['c' 3] ['d' 4] ['e' 5] ~])
    ~zod/try=> (~(all by a) |=(a=@ (lte a 6)))
    %.y
    ~zod/try=> (~(all by a) |=(a=@ (lte a 4)))
    %.n

---

###+-any:by


```
  +-  any                                               ::  logical OR
    ~/  %any
    |*  b=$+(* ?)
    |-  ^-  ?
    ?~  a
      |
    ?|((b q.n.a) $(a l.a) $(a r.a))
  ::
```

A value in the map matches a predicate.

    ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
    ~zod/try=> (~(all by b) |=(a=* ?@(a & |)))
    %.y
    ~zod/try=> =a (mo `(list ,[@t @u])`[['a' 1] ['b' 2] ['c' 3] ['d' 4] ['e' 5] ~])
    ~zod/try=> (~(any by a) |=(a=@ (lte a 4)))
    %.y

---

###+-del:by


```
  +-  del                                               ::  delete at key b
    ~/  %del
    |*  b=*
    |-  ^+  a
    ?~  a
      ~
    ?.  =(b p.n.a)
      ?:  (gor b p.n.a)
        [n.a $(a l.a) r.a]
      [n.a l.a $(a r.a)]
    |-  ^-  ?(~ _a)
    ?~  l.a  r.a
    ?~  r.a  l.a
    ?:  (vor p.n.l.a p.n.r.a)
      [n.l.a l.l.a $(l.a r.l.a)]
    [n.r.a $(r.a l.r.a) r.r.a]
  ::
```

Accept a noun and removes it as a key from the map.

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
        ~zod/try=> (~(del by b) `a`)
        {[p=`b` q=[2 3]]}
        
---

###+-dig:by


```
  +-  dig                                               ::  axis of b key
    |=  b=*
    =+  c=1
    |-  ^-  (unit ,@)
    ?~  a  ~
    ?:  =(b p.n.a)  [~ u=(peg c 2)]
    ?:  (gor b p.n.a)
      $(a l.a, c (peg c 6))
    $(a r.a, c (peg c 7))
  ::
```


Produce the axis of a key within the set.

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])  
        ~zod/try=> (~(dig by b) `b`)
        [~ 2]

---

###+-gas:by


```
  +-  gas                                               ::  concatenate
    ~/  %gas
    |*  b=(list ,[p=* q=*])
    =>  .(b `(list ,_?>(?=(^ a) n.a))`b)
    |-  ^+  a
    ?~  b
      a
    $(b t.b, a (put(+< a) p.i.b q.i.b))
  ::
```

Insert a list of key-value pairs into the map.

    ~zod/try=> =a (mo `(list ,[@t *])`[[`a` 1] [`b` 2] ~])
    ~zod/try=> =b `(list ,[@t *])`[[`c` 3] [`d` 4] ~]
    ~zod/try=> (~(gas by a) b)
    {[p=`d` q=4] [p=`a` q=1] [p=`c` q=3] [p=`b` q=2]}

---

###+-get:by


```
  +-  get                                               ::  grab value by key
    ~/  %get
    |*  b=*
    |-  ^-  ?(~ [~ u=_?>(?=(^ a) q.n.a)])
    ?~  a
      ~
    ?:  =(b p.n.a)
      [~ u=q.n.a]
    ?:  (gor b p.n.a)
      $(a l.a)
    $(a r.a)
  ::
```

Unit value in the map at a key(if it exists).

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])  
        ~zod/try=> (~(get by b) `b`)
        [~ [2 3]]

---

###+-got:by


```
  +-  got
    |*  b=*
    %-  need
    %-  get(+< a)  b
  ::
```

Value in the map at a key, crashing on inexistance.

        ~zod/try=> =m (mo `(list ,[@t *])`[['a' 1] ['b' 2] ~])
        ~zod/try=> m
        {[p='a' q=1] [p='b' q=2]}
        ~zod/try=> (~(get by m) 'a')
        [~ 1]
        ~zod/try=> (~(got by m) 'a')
        1
        ~zod/try=> (~(got by m) 'c')
        ! exit

---

###+-has:by


```
  +-  has                                               ::  key existence check
    ~/  %has
    |*  b=*
    !=(~ (get(+< a) b))
  ::
```

Whether a noun is a key in the map.

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])  
        ~zod/try=> (~(has by b) `b`)
        %.y
        ~zod/try=> (~(has by b) `c`)
        %.n

---

###+-int:by


```
  +-  int                                               ::  intersection
    ~/  %int
    |*  b=_a
    |-  ^+  a
    ?~  b
      ~
    ?~  a
      ~
    ?:  (vor p.n.a p.n.b)
      ?:  =(p.n.b p.n.a)
        [n.b $(a l.a, b l.b) $(a r.a, b r.b)]
      ?:  (hor p.n.b p.n.a)
        %-  uni(+< $(a l.a, b [n.b l.b ~]))  $(b r.b)
      %-  uni(+< $(a r.a, b [n.b ~ r.b]))  $(b l.b)
    ?:  =(p.n.a p.n.b)
      [n.b $(b l.b, a l.a) $(b r.b, a r.a)]
    ?:  (hor p.n.a p.n.b)
      %-  uni(+< $(b l.b, a [n.a l.a ~]))  $(a r.a)
    %-  uni(+< $(b r.b, a [n.a ~ r.a]))  $(a l.a)
  ::
```

Produce the intersection between the map and another of the same type.

        ~zod/try=> =n (mo `(list ,[@t *])`[['a' 1] ['c' 3] ~])
        ~zod/try=> n
        {[p='a' q=1] [p='c' q=3]}
        ~zod/try=> m
        {[p='a' q=1] [p='b' q=2]}
        ~zod/try=> (~(int by m) n)
        {[p='a' q=1]}
        ~zod/try=> =o (mo `(list ,[@t *])`[['c' 3] ['d' 4] ~])
        ~zod/try=> (~(int by m) o)
        {}
       
---

###+-mar:by


```
  +-  mar                                               ::  add with validation
    |*  [b=_?>(?=(^ a) p.n.a) c=(unit ,_?>(?=(^ a) q.n.a))]
    ?~  c
      (del b)
    (put b u.c)
  ::
```

Accept a noun and a unit of a noun of the type of the map's keys and values, respectively. 
Validate that the value is not null and put the pair in the map. If the value is null, 
delete the key.

XX This arm is broken, asana task 15186618346453

        ~zod/try=> m
        {[p='a' q=1] [p='b' q=2]}
        ~zod/try=> (~(mar by m) 'c' (some 3))
        ! -find-limb.n
        ! find-none
        ! exit
        ~zod/try=> (~(mar by m) 'c' ~)
        ! -find-limb.n
        ! find-none
        ! exit
        ~zod/try=> (~(mar by m) 'b' ~)
        ! -find-limb.n
        ! find-none
        ! exit

---

###+-put:by


```
  +-  put                                               ::  adds key-value pair
    ~/  %put
    |*  [b=* c=*]
    |-  ^+  a
    ?~  a
      [[b c] ~ ~]
    ?:  =(b p.n.a)
      ?:  =(c q.n.a)
        a
      [[b c] l.a r.a]
    ?:  (gor b p.n.a)
      =+  d=$(a l.a)
      ?>  ?=(^ d)
      ?:  (vor p.n.a p.n.d)
        [n.a d r.a]
      [n.d l.d [n.a r.d r.a]]
    =+  d=$(a r.a)
    ?>  ?=(^ d)
    ?:  (vor p.n.a p.n.d)
      [n.a l.a d]
    [n.d [n.a l.a l.d] r.d]
  ::
```

Add a key-value pair to the map.

    ~zod/try=> m
    {[p='a' q=1] [p='b' q=2]}
    ~zod/try=> (~(put by m) 'c' 3)
    {[p='a' q=1] [p='c' q=3] [p='b' q=2]}
    ~zod/try=> (~(put by m) "zod" 26)
    ! type-fail
    ! exit
    ~zod/try=> (~(put by m) 'a' 2)
    {[p='a' q=2] [p='b' q=2]}

---

###+-rep:by


```
  +-  rep                                               ::  replace by product
    |*  [b=* c=_,*]
    |-
    ?~  a  b
    $(a r.a, b $(a l.a, b (c q.n.a b)))
  ::
```

Accumulate using gate from values in map

XX interface changing.
   
   

---

        
###+-rib:by


```
  +-  rib                                               ::  transform + product
    |*  [b=* c=_,*]
    |-  ^+  [b a]
    ?~  a  [b ~]
    =+  d=(c n.a b)
    =.  n.a  +.d
    =+  e=$(a l.a, b -.d)
    =+  f=$(a r.a, b -.e)
    [-.f [n.a +.e +.f]]
  ::
```

Replace values with accumulator 

XX interface changing, possibly disappearing

---
        
###+-run:by


```
  +-  run                                               ::  turns to tuples
    |*  b=_,*
    |-  
    ?~  a  a
    a(n (b q.n.a), l $(a l.a), r $(a r.a))
  ::
```

Apply gate to values in map.

    ~zod/try=> m
    {[p='a' q=1] [p='b' q=2]}
    ~zod/try=> ^+(m (~(run by m) dec))
    {[p='a' q=0] [p='b' q=1]}
    ~zod/try=> `(map ,@tas ,@t)`(~(run by m) (cury scot %ux))
    {[p=%a q='0x1'] [p=%b q='0x2']}

---

###+-tap:by


```
  +-  tap                                               ::  listify pairs
    ~/  %tap
    |=  b=(list ,_?>(?=(^ a) n.a))
    ^+  b
    ?~  a
      b
    $(a r.a, b [n.a $(a l.a)])
  ::
```

    {[p='a' q=1] [p='b' q=2]}
    ~zod/try=> `*`m
    [[98 2] [[97 1] 0 0] 0]
    ~zod/try=> (~(tap by m))
    ~[[p='b' q=2] [p='a' q=1]]
    ~zod/try=> `*`(~(tap by m))
    [[98 2] [97 1] 0]


---

###+-uni:by


```
  +-  uni                                               ::  union, merge
    ~/  %uni
    |*  b=_a
    |-  ^+  a
    ?~  b
      a
    ?~  a
      b
    ?:  (vor p.n.a p.n.b)
      ?:  =(p.n.b p.n.a)
        [n.b $(a l.a, b l.b) $(a r.a, b r.b)]
      ?:  (hor p.n.b p.n.a)
        $(a [n.a $(a l.a, b [n.b l.b ~]) r.a], b r.b)
      $(a [n.a l.a $(a r.a, b [n.b ~ r.b])], b l.b)
    ?:  =(p.n.a p.n.b)
      [n.b $(b l.b, a l.a) $(b r.b, a r.a)]
    ?:  (hor p.n.a p.n.b)
      $(b [n.b $(b l.b, a [n.a l.a ~]) r.b], a r.a)
    $(b [n.b l.b $(b r.b, a [n.a ~ r.a])], a l.a)
  ::
```

Produce the union between two maps.

    ~zod/try=> m
    {[p='a' q=1] [p='b' q=2]}
    ~zod/try=> o
    {[p='d' q=4] [p='c' q=3]}
    ~zod/try=> (~(uni by m) o)
    {[p='d' q=4] [p='a' q=1] [p='c' q=3] [p='b' q=2]}
    ~zod/try=> (~(uni by m) ~)
    {[p='a' q=1] [p='b' q=2]}
    ~zod/try=> n
    {[p='a' q=1] [p='c' q=3]}
    ~zod/try=> (~(uni by o) n)
    {[p='d' q=4] [p='a' q=1] [p='c' q=3]}

---

###+-urn:by


```
  +-  urn                                               ::  turn
    |*  b=$+([* *] *)
    |-
    ?~  a  ~
    [n=[p=p.n.a q=(b p.n.a q.n.a)] l=$(a l.a) r=$(a r.a)]
  ::
```

Turn over the values of the map and produce the tranformed map.

    ~zod/try=> m
    {[p='a' q=1] [p='b' q=2]}
    ~zod/try=> (~(urn by m) |=(a=[p=* q=*] q.a))
    {[p='a' q=1] [p='b' q=2]}
    ~zod/try=> (~(urn by m) |=(a=[p=* q=*] 7))
    {[p='a' q=7] [p='b' q=7]}
    ~zod/try=> (~(urn by m) |=(a=[p=* q=*] p.a))
    {[p='a' q=97] [p='b' q=98]}

---

###+-wyt:by


```
  +-  wyt                                               ::  depth of map
    .+
    |-  ^-  @
    ?~(a 0 +((add $(a l.a) $(a r.a))))
```

Produce the depth of the tree map.

    ~zod/try=> m
    {[p='a' q=1] [p='b' q=2]}
    ~zod/try=> o
    {[p='d' q=4] [p='c' q=3]}
    ~zod/try=> ~(wyt by m)
    3
    ~zod/try=> ~(wyt by o)
    3
    ~zod/try=> ~(wyt by (~(uni by m) o))
    5

---
