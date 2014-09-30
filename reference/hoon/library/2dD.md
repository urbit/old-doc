section 2dD, casual containers        

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

Mapifiy.  Accepts a list of cells and produces a map of key-value pairs from the left-right cell pairs of the list.

####Summary

        Creates a wet %gold gate which accepts a list, 'a'.
        Pushes the homogenized list onto the context.
        Casts the list 'a' to a list of cells whose left-right types correspond to the key-value type pairs.
        Let 'b' be the bunt of the map with the properly typed keys and values from the cell at the head of our list.
        Concatenate the elements of 'a' into the empty map of bunt 'b', and produce the result.

####Examples

        ~talsur-todres/try=> (mo `(list ,[@t *])`[[`a` 1] [`b` 2] ~])
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

####Summary

        Creates a wet %gold gate which accepts a list, 'a'.
        Pushes the homogenized list onto the context.
        Let 'b' be the bunt of the set with elements of the same type of the elements of 'a'.
        Concatenate the elements of 'a' into the empty set of bunt 'b', and produce the result.

####Examples

        ~talsur-todres/try=> (sa `(list ,@)`[1 2 3 4 5 ~])
        {5 4 1 3 2}
        ---
        ~talsur-todres/try=> (sa `(list ,[@t *])`[[`a` 1] [`b` 2] ~])
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

####Summary

####Examples

---


