##section 2dD, casual containers        

---

###++mo


```
++  mo                                                  ::  make a map
  |*  a=(list)
  =>  .(a `_(homo a)`a)
  =>  .(a `(list ,[p=_-<.a q=_->.a])`a)
  =+  b=*(map ,_?>(?=(^ a) p.i.a) ,_?>(?=(^ a) q.i.a))
  (~(gas by b) a)
::
```


Mapifiy.  Accepts a list of cells and produces a map of key-value pairs from the 
left-right cell pairs of the list.

    ~zod/try=> (mo `(list ,[@t *])`[[`a` 1] [`b` 2] ~])
    {[p=`a` q=1] [p=`b` q=2]}

----
        
###++sa        


```
++  sa                                                  ::  make a set
  |*  a=(list)
  =>  .(a `_(homo a)`a)
  =+  b=*(set ,_?>(?=(^ a) i.a))
  (~(gas in b) a)
::
```


Setify.  Accepts a list and produces a set of the list's elements.

    ~zod/try=> (sa `(list ,@)`[1 2 3 4 5 ~])
    {5 4 1 3 2}
    ~zod/try=> (sa `(list ,[@t *])`[[`a` 1] [`b` 2] ~])
    {[`a` 1] [`b` 2]}

----

###++qu


```
++  qu                                                  ::  make a set
  |*  a=(list)
  =>  .(a `_(homo a)`a)
  =+  b=*(set ,_?>(?=(^ a) i.a))
  (~(gas in b) a)
```


XXX THIS APPEARS TO BE A COPY OF ++sa. QUEUIFY IS NOT IMPLEMENTED YET. XXX

    ~zod/try=> (qu `(list ,@ud)`~[1 2 3 5])
    {5 3 2 1}
    ~zod/try=> (qu "sada")
    {'a' 'd' 'a' 's'}
    ~zod/try=> ~(top to (qu "sada"))
    [~ 's']

---


