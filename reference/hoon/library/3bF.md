##section 3bF, filesystem interface

###++fain

```
++  fain                                                ::  path restructure
  |=  [hom=path raw=path]
  =+  bem=(need (tome raw))
  =+  [mer=(flop s.bem) moh=(flop hom)]
  |-  ^-  (pair beam path)
  ?~  moh
    [bem(s hom) (flop mer)]
  ?>  &(?=(^ mer) =(i.mer i.moh))
  $(mer t.mer, moh t.moh)
::
```

XX  Document

###++feel

```
++  feel                                                ::  simple file write
  |=  [pax=path val=*]
  ^-  miso
  =+  dir=((hard arch) .^(%cy pax))
  ?~  q.dir  [%ins val]
  :-  %mut
  ^-  udon
  [%a %a .^(%cx pax) val]
::
```

XX  Document

###++file

```
++  file                                                ::  simple file load
  |=  pax=path
  ^-  (unit)
  =+  dir=((hard arch) .^(%cy pax))
  ?~(q.dir ~ [~ .^(%cx pax)])
::
```

XX  Document

###++foal

```
++  foal                                                ::  high-level write
  |=  [pax=path val=*]
  ^-  toro
  ?>  ?=([* * * *] pax)
  [i.t.pax [%& [*cart [[t.t.t.pax (feel pax val)] ~]]]]
::
```

XX  Document

###++fray

```
++  fray                                                ::  high-level delete
  |=  pax=path
  ^-  toro
  ?>  ?=([* * * *] pax)
  [i.t.pax [%& [*cart [[t.t.t.pax [%del .^(%cx pax)]] ~]]]]
::
```

XX  Document

###++furl

```
++  furl                                                ::  unify changes
  |=  [one=toro two=toro]
  ^-  toro
  ~|  %furl
  ?>  ?&  =(p.one p.two)                                ::  same path
          &(?=(& -.q.one) ?=(& -.q.two))                ::  both deltas
      ==
  [p.one [%& [*cart (weld q.q.q.one q.q.q.two)]]]
::
```

XX  Document

###++meat

```
++  meat                                                ::  kite to .^ path
  |=  kit=kite
  ^-  path
  [(cat 3 'c' p.kit) (scot %p r.kit) s.kit (scot `dime`q.kit) t.kit]
::
```

XX  Document

###++tame

```
++  tame                                                ::  parse kite path
  |=  hap=path
  ^-  (unit kite)
  ?.  ?=([@ @ @ @ *] hap)  ~
  =+  :*  hyr=(slay i.hap)
          fal=(slay i.t.hap)
          dyc=(slay i.t.t.hap)
          ved=(slay i.t.t.t.hap)
          ::  ved=(slay i.t.hap)
          ::  fal=(slay i.t.t.hap)
          ::  dyc=(slay i.t.t.t.hap)
          tyl=t.t.t.t.hap
      ==
  ?.  ?=([~ %$ %tas @] hyr)  ~
  ?.  ?=([~ %$ %p @] fal)  ~
  ?.  ?=([~ %$ %tas @] dyc)  ~
  ?.  ?=([~ %$ case] ved)  ~
  =+  his=`@p`q.p.u.fal
  =+  [dis=(end 3 1 q.p.u.hyr) rem=(rsh 3 1 q.p.u.hyr)]
  ?.  ?&(?=(%c dis) ?=(?(%v %w %x %y %z) rem))  ~
  [~ rem p.u.ved q.p.u.fal q.p.u.dyc tyl]
::
```

XX  Document

###++tome

```
++  tome                                                ::  parse path to beam
  |=  pax=path
  ^-  (unit beam)
  ?.  ?=([* * * *] pax)  ~
  %+  biff  (slaw %p i.pax)
  |=  who=ship
  %+  biff  (slaw %tas i.t.pax)
  |=  dex=desk
  %+  biff  (slay i.t.t.pax)
  |=  cis=coin
  ?.  ?=([%$ case] cis)  ~
  `(unit beam)`[~ [who dex `case`p.cis] (flop t.t.t.pax)]
::
```

XX  Document

###++tope
