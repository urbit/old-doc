section 2dC, queues                   

###++to

```
++  to                                                  ::  queue engine
  |/  a=(qeu)
```

Container arm for queue operation arms.  The contained arms inherit it's sample queue, 'a'. 

##+-  bal

Walks through the queue using vor (v-order check) on all eleements.

####Examples

        ~palryp-hocsyt/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[6 1 3 6 1 3 4 6 ~])
        ~palryp-hocsyt/try=> a
        {6 4 3 1 6 3 1 6}
        ~palryp-hocsyt/try=> ~(bal to a)
        {6 4 3 1 6 3 1 6}
        
---

##+-  dep

Produce the maximum depth of leaves (r.a and l.a) in the queue 'a'.

####Examples

        ~palryp-hocsyt/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 4 5 6 7 ~])
        ~palryp-hocsyt/try=> ~(dep to a)
        4
        ---
        ~palryp-hocsyt/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 4 ~])
        ~palryp-hocsyt/try=> ~(dep to a)
        3
        ---
        ~palryp-hocsyt/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 ~])
        ~palryp-hocsyt/try=> ~(dep to a)
        2

---

##+-  gas

Accept a list `b` of elements of the type of the queue `a` elements and produce the queue
`a` with the elements of `b` added.

####Examples

        ~palryp-hocsyt/try=> (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 ~])
        {3 2 1}
        ---
        ~palryp-hocsyt/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 ~])
        ~palryp-hocsyt/try=> =b `(list ,@)`[4 5 6 ~]
        ~palryp-hocsyt/try=> (~(gas to a) b)
        {6 5 4 3 2 1}

---

##+-  get

Produces the queue 'a' in the format [p=head q=tail].

####Examples

---

##+-  nap

Remove the head of a queue and produce the resulting queue.

####Examples

        ~talsur-todres/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 4 5 6 ~])
        ~talsur-todres/try=> -.a
        n=6
        ~talsur-todres/try=> =b ~(nap to a)
        ~talsur-todres/try=> -.b
        n=2
        ~talsur-todres/try=> b
        {5 4 3 2 1}
        ~talsur-todres/try=> a
        {6 5 4 3 2 1}

---

##+-  put

Accept any noun and adds to the queue as the head, producing the resutling queue.

####Examples

        ~dovryp-toblug/try=> (~(gas to `(qeu ,@)`~) `(list ,@)`[3 1 2 4 5 6 ~])
        ~dovryp-toblug/try=> (~(put to a) 7)
        {7 6 5 4 2 1 3}

---

  +-  tap

Concatenates two lists from the first

#### Examples

        ~dovryp-toblug/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[3 1 2 4 5 6 ~])
        ~dovryp-toblug/try=> (~(tap to a) `(list ,@)`[99 100 101 ~])
        ~[3 1 2 4 5 6 99 100 101]

---

##+-  top

####Examples

        ~talsur-todres/try=> =a (~(gas to `(qeu ,@)`~) `(list ,@)`[1 2 3 4 5 6 ~])
        ~talsur-todres/try=> ~(top to a)
        [~ 1]

---


