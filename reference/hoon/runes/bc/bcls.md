#buclus `$+` %bcls

[Short description]

#Syntax

`$+`, `buclus`, a tile for a gate which accepts `p` and produces `q`. The spectre of function signatures once again rears its ugly head - but `$+(p q)` is no different from `$_(|+(p _q))`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

$+  p  q

##Wide form

$+(p q)

##Irregular form

None

##Examples

++  sort                                                ::  quicksort
      ~/  %sort
      !:
      |*  [a=(list) b=$+([* *] ?)]
      =>  .(a ^.(homo a))
      |-  ^+  a
      ?~  a  ~
      %+  weld
        $(a (skim t.a |=(c=_i.a (b c i.a))))
      ^+  t.a
      [i.a $(a (skim t.a |=(c=_i.a !(b c i.a))))]

In ++sort, `$+` is a tile for a comparator gate, which takes two nouns and produces a loobean.

