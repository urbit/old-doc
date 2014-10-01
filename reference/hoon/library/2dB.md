section 2dB, maps
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

####Examples

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
The contained arms inherit the sample jar. 'a'.

        Build a wet %gold tray with a sample jar `a`...

---

##+-  get

Retrieve a list from the map by its key.

####Examples
 
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

##+-  add

Add a key-list value to the jar.

####Examples

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

      Terminate the core.

---

###++ju

```
++  ju                                                  ::  jug engine
  |/  a=(jug)
```

The jug engine: container arm for jug operation arms.  Jugs are maps of sets.
The contained arms inherit it's sample jug, 'a'.

        Build a wet %gold tray with a sample jug `a`.

##+-  del
        
Delete a value in a set and produce the resulting jug.

####Examples

      ~zod/try=> s
      {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}
      ~zod/try=> (~(del ju s) 'a' 1)
      {[p='a' q={3 2}] [p='b' q={5 4 6}]}
      ~zod/try=> (~(del ju s) 'c' 7)
      {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}        

---

+-  get

Retrieve a set from the map by its key.

####Examples

      ~zod/try=> s
      {[p='a' q={1 3 2}] [p='b' q={5 4 6}]}
      ~zod/try=> (~(get ju s) 'a')
      {1 3 2}
      ~zod/try=> (~(get ju s) 'b')
      {5 4 6}
      ~zod/try=> (~(get ju s) 'c')
      ~
      
---

##+-  has

Is the element `c` in the set `b`?

####Examples

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

##+-  put

Add a value to a specific set in the jug.

####Examples

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

##+-  all

Accept a gate which accepts any noun and produces a loobean.  Slams the gate with each member
of map 'a', produce the logical AND of the transformed map.

####Examples
 
        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
        ~zod/try=> (~(all by b) |=(a=* ?@(a & |)))
        %.n
        ---
        ~zod/try=> =a (mo `(list ,[@t @u])`[['a' 1] ['b' 2] ['c' 3] ['d' 4] ['e' 5] ~])
        ~zod/try=> (~(all by a) |=(a=@ (lte a 6)))
        %.y
        ~zod/try=> (~(all by a) |=(a=@ (lte a 4)))
        %.n

---

##+-  any

Accept a gate which accepts any noun and produces a loobean.  Slam the gate with each member
of map 'a' and produce the logical OR of the transformed map.

####Examples

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
        ~zod/try=> (~(all by b) |=(a=* ?@(a & |)))
        %.y
        ---
        ~zod/try=> =a (mo `(list ,[@t @u])`[['a' 1] ['b' 2] ['c' 3] ['d' 4] ['e' 5] ~])
        ~zod/try=> (~(any by a) |=(a=@ (lte a 4)))
        %.y

---

##+-  del

Accept a noun 'b', producing the map with the key-value pair of key 'b' removed.

####Examples

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])
        ~zod/try=> (~(del by b) `a`)
        {[p=`b` q=[2 3]]}
        
---

##+-  dig

Accept any noun 'b' and produce the axis of 'b' in within the values of 'p.a' in map 'a'.

####Examples

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])  
        ~zod/try=> (~(dig by b) `b`)
        [~ 2]

---

##+-  gas

Accept any list 'b' of key-value pair cells and produce the map 'a'
with the members of 'b' added.

####Examples

        ~zod/try=> =a (mo `(list ,[@t *])`[[`a` 1] [`b` 2] ~])
        ~zod/try=> =b `(list ,[@t *])`[[`c` 3] [`d` 4] ~]
        ~zod/try=> (~(gas by a) b)
        {[p=`d` q=4] [p=`a` q=1] [p=`c` q=3] [p=`b` q=2]}

---

##+-  get

Produce the value in the map at key 'b'.

####Examples

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])  
        ~zod/try=> (~(get by b) `b`)
        [~ [2 3]]

---

##+-  got

####Examples

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

##+-  has

Accept any noun 'b' and produces the loobean indicating whether the noun exists in map 'a'.

####Examples

        ~zod/try=> =b (mo `(list ,[@t *])`[['a' 1] ['b' [2 3]] ~])  
        ~zod/try=> (~(has by b) `b`)
        %.y
        ~zod/try=> (~(has by b) `c`)
        %.n

---

##+-  int

Produce the intersection of two maps of the same type.

        Where uni(+< $(b r.b, b [n.b ~ r.b])) is the call of uni with the map
        replaced by the toss of `b` for `r.b` and `b` for [n.b ~ r.b].

####Examples

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

##+-  mar

Accept a noun and a unit of a noun of the type of the map's keys and values, respectively. 
Validate that the value is not null and put the pair in the map. If the value is null, 
delete the key.

####Examples

        XXX This arm appears to be broken.
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

##+-  put

Add a key-value pair to the map.

        Creates and kicks a dry %gold trap.  Casts the result to the type of the map 'a'.
        If "a is an atom", produce the cell [[b c] ~ ~].
        Else, build the if-then-else statement if

####Examples

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

##+-  rep

Walk through the map, replacing 'b' with the product of (c n.a b).  Produce the resulting
map.

####Examples

---

        
##+-  rib

Walk throught the map, replacing the values n.a with the product of (c n.a b) and produce
the transformed map with the accumulated. `b`.


####Examples


---
        
##+-  run

---

##+-  tap

---

##+-  uni

Produce the union between two maps.

####Examples

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

##+-  urn

Turn over the values of the map and produce the tranformed map.

####Examples

        ~zod/try=> m
        {[p='a' q=1] [p='b' q=2]}
        ~zod/try=> (~(urn by m) |=(a=[p=* q=*] q.a))
        {[p='a' q=1] [p='b' q=2]}
        ~zod/try=> (~(urn by m) |=(a=[p=* q=*] 7))
        {[p='a' q=7] [p='b' q=7]}
        ~zod/try=> (~(urn by m) |=(a=[p=* q=*] p.a))
        {[p='a' q=97] [p='b' q=98]}

---

##+-  wyt

Produce the depth of the tree map.

####Examples

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


