##section 2dC, queues

---

###++to


```
++  to                                                  ::  queue engine
  |/  a=(qeu)
```


Container arm for queue operation arms.  The contained arms inherit it's sample queue, 'a'. 

###+-bal


```
  +-  bal
    |-  ^+  a
    ?~  a  ~
    ?.  |(?=(~ l.a) (vor n.a n.l.a))
      $(a [n.l.a l.l.a $(a [n.a r.l.a r.a])])
    ?.  |(?=(~ r.a) (vor n.a n.r.a))
      $(a [n.r.a $(a [n.a l.a l.r.a]) r.r.a])
    a
  ::
```

Vertically rebalance queue

    ~zod/try=> `(qeu tape)`["a" ~ "b" ~ "c" ~ "d" ~ "e" ~ "f" ~ "g" ~ ~]
    {"a" "b" "c" "d" "e" "f" "g"}
    ~zod/try=> `*`["a" ~ "b" ~ "c" ~ "d" ~ "e" ~ "f" ~ "g" ~ ~]
    [[97 0] 0 [98 0] 0 [99 0] 0 [100 0] 0 [101 0] 0 [102 0] 0 [103 0] 0 0]
    ~zod/try=> ~(bal to `(qeu tape)`["a" ~ "b" ~ "c" ~ "d" ~ "e" ~ "f" ~ "g" ~ ~])
    {"a" "b" "c" "d" "e" "f" "g"}
    ~zod/try=> `*`~(bal to `(qeu tape)`["a" ~ "b" ~ "c" ~ "d" ~ "e" ~ "f" ~ "g" ~ ~])
    [[100 0] [[99 0] [[98 0] [[97 0] 0 0] 0] 0] [101 0] 0 [102 0] 0 [103 0] 0 0]
    
---

###+-dep


```
  +-  dep                                               ::  max depth of queue
    |-  ^-  @
    ?~  a  0
    +((max $(a l.a) $(a r.a)))
  ::
```

Produce the maximum depth of leaves (r.a and l.a) in the queue 'a'.

    ~zod/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 4 5 6 7 ~])
    ~zod/try=> ~(dep to a)
    4
    ~zod/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 4 ~])
    ~zod/try=> ~(dep to a)
    3
    ~zod/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 ~])
    ~zod/try=> ~(dep to a)
    2

    ~zod/try=> ~(dep to `(qeu tape)`["a" ~ "b" ~ "c" ~ "d" ~ "e" ~ "f" ~ "g" ~ ~])
    7
    ~zod/try=> ~(dep to ~(bal to `(qeu tape)`["a" ~ "b" ~ "c" ~ "d" ~ "e" ~ "f" ~ "g" ~ ~]))
    4


---

###+-gas


```
  +-  gas                                               ::  insert list to que
    |=  b=(list ,_?>(?=(^ a) n.a))
    |-  ^+  a
    ?~(b a $(b t.b, a (put(+< a) i.b)))
  ::
```

Push all elements of list into the queue.

    ~zod/try=> (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 ~])
    {3 2 1}
    ~zod/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 ~])
    ~zod/try=> =b `(list ,@)`[4 5 6 ~]
    ~zod/try=> (~(gas to a) b)
    {6 5 4 3 2 1}

---

###+-get


```
  +-  get                                               ::  head-tail pair
    |-  ^+  [p=?>(?=(^ a) n.a) q=a]
    ?~  a
      !!
    ?~  r.a
      [n.a l.a]
    =+  b=$(a r.a)
    :-  p.b
    ?:  |(?=(~ q.b) (vor n.a n.q.b))
      [n.a l.a q.b]
    [n.q.b [n.a l.a l.q.b] r.q.b]
  ::
```

Produces the head element and tail queue.

---

###+-nap


```
  +-  nap                                               ::  removes head
    ?>  ?=(^ a)
    ?:  =(~ l.a)  r.a
    =+  b=get(+< l.a)
    bal(+< ^+(a [p.b q.b r.a]))
  ::
```

Remove the head of a queue and produce the resulting queue.

    ~zod/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 4 5 6 ~])
    ~zod/try=> -.a
    n=6
    ~zod/try=> =b ~(nap to a)
    ~zod/try=> -.b
    n=2
    ~zod/try=> b
    {5 4 3 2 1}
    ~zod/try=> a
    {6 5 4 3 2 1}

---

###+-put


```
  +-  put                                               ::  insert new tail
    |*  b=*
    |-  ^+  a
    ?~  a
      [b ~ ~]
    bal(+< a(l $(a l.a)))
  ::
```

Accept any noun and adds to the queue as the head, producing the resulting queue.

    ~zod/try=> (~(gas to `(qeu ,@)`~) `(list ,@)`[3 1 2 4 5 6 ~])
    ~zod/try=> (~(put to a) 7)
    {7 6 5 4 2 1 3}

---

###+-tap

```
  +-  tap                                               ::  adds list to end
    |=  b=(list ,_?>(?=(^ a) n.a))
    ^+  b
    ?~  a
      b
    $(a r.a, b [n.a $(a l.a)])
  ::
```

Flattens queue into a list

    ~zod/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[3 1 2 4 5 6 ~])
    ~zod/try=> `*`a
    [6 0 2 [4 [5 0 0] 0] 1 0 3 0 0]
    ~zod/try=> (~(tap to a) `(list ,@)`[99 100 101 ~])
    ~[3 1 2 4 5 6 99 100 101]

---

###+-top


```
  +-  top                                               ::  produces head
    |-  ^-  (unit ,_?>(?=(^ a) n.a))
    ?~  a  ~
    ?~(r.a [~ n.a] $(a r.a))
```

Unit top of queue

    ~zod/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 4 5 6 ~])
    ~zod/try=> ~(top to a)
    [~ 1]

---


