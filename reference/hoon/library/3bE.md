##section 3bE, tree sync

###++invert

``````

XX document

###++cosh

```
++  cosh                                                ::  locally rehash
  |=  ank=ankh                                          ::  NB v/unix.c
  ank(p rehash:(zu ank))
::
```

XX document

###++cost

```
++  cost                                                ::  new external patch
  |=  [bus=ankh ank=ankh]                               ::  NB v/unix.c
  ^-  soba
  :-  [p.ank p.bus] 
  %-  flop
  myz:(change-tree:(zu ank) %c bus)
::
```

XX document

###++loth

```
++  loth
  |=  pat=(map path ,*)
  ^-  (set path)
  %+  roll  (~(tap by pat) ~)
  |=  [[p=path *] q=(set path)]
  %.  p  %~  put  in  q
::
```

XX document

###++luth

```
++  luth
  |=  [p=(map path ,*) q=(map path ,*)]                 ::  merge keysets
  ^-  (set path)
  (~(uni in (loth p)) (loth q))
::
```

XX document

###++blob

``````

XX document

###++ze

```
++  ze
  |_  [lim=@da dome rang]
```

XX document

###++aeon

``````

XX document

###++aeon

``````

XX document

###++make

``````

XX document

###++tako

``````

XX document

###++lobe

``````

XX document

###++lobe

``````

XX document

###++make

``````

XX document

###++make

``````

XX document

###++blob

``````

XX document

###++blob

``````

XX document

###++diff

``````

XX document

###++lobes

``````

XX document

###++case

``````

XX document

###++as

``````

XX document

###++reachable

``````

XX document

###++new

``````

XX document

###++new

``````

XX document

###++reachable

``````

XX document

###++takos

``````

XX document

###++lobes

``````

XX document

###++make

``````

XX document

###++query

```
  ++  query                                             ::    query:ze
    |=  ren=?(%u %v %x %y %z)                           ::  endpoint query
    ^-  (unit ,*)
    ?-  ren
      %u  [~ `rang`+<+>.query]
      %v  [~ `dome`+<+<.query]
      %x  ?~(q.ank ~ [~ q.u.q.ank])
      %y  [~ as-arch]
      %z  [~ ank]
    ==
  ::
```

XX document

###++rewind

```
  ++  rewind                                            ::    rewind:ze
    |=  yon=aeon                                        ::  rewind to aeon
    ^+  +>
    ?:  =(let yon)  +>
    ?:  (gth yon let)  !!                               ::  don't have version
    +>(ank (checkout-ankh q:(aeon-to-yaki yon)), let yon)
  ::
```

XX document

###++update

``````

XX document

###++apply

``````

XX document

###++checkout

``````

XX document

###++forge

```
  ++  forge                                         ::  %forge
    |=  [p=yaki q=yaki s=[ship desk] t=[ship desk]]
    ^-  (map path blob)
    =+  r=(~(tap in (find-merge-points p q)) ~)
    ?~  r
      ~|(%forge-no-ancestor !!)
    %-  |=  [r=yaki lut=(map lobe blob) hat=(map tako yaki)]
        =.  lat  lut
        =.  hut  hat
        (meld p q r & s t)                          ::  fake merge
    %+  roll  t.r                                   ::  fake ancestor
    |=  [par=yaki [for=_i.r lut=_lat hat=_hut]]
    =.  lat  lut
    =+  ^=  far
        ^-  (map path lobe)
        %-  ~(tur by (forge par for s t))
        |=  [k=path v=blob]  (blob-to-lobe v)
    =+  u=(make-yaki [r.par r.for ~] far `@da`0)    ::  fake yaki
    :-  u
    :_  (~(put by hat) r.u u)
    =<  -
    %-  update-lat
    :_  ~
    %-  ~(tur by q.u)
    |=  [path k=lobe]
    (lobe-to-blob k)
  ::
  ::  actual merge
  ::
```

XX document

###++forge

```
  ++  forge                                         ::  %forge
    |=  [p=yaki q=yaki s=[ship desk] t=[ship desk]]
    ^-  (map path blob)
    =+  r=(~(tap in (find-merge-points p q)) ~)
    ?~  r
      ~|(%forge-no-ancestor !!)
    %-  |=  [r=yaki lut=(map lobe blob) hat=(map tako yaki)]
        =.  lat  lut
        =.  hut  hat
        (meld p q r & s t)                          ::  fake merge
    %+  roll  t.r                                   ::  fake ancestor
    |=  [par=yaki [for=_i.r lut=_lat hat=_hut]]
    =.  lat  lut
    =+  ^=  far
        ^-  (map path lobe)
        %-  ~(tur by (forge par for s t))
        |=  [k=path v=blob]  (blob-to-lobe v)
    =+  u=(make-yaki [r.par r.for ~] far `@da`0)    ::  fake yaki
    :-  u
    :_  (~(put by hat) r.u u)
    =<  -
    %-  update-lat
    :_  ~
    %-  ~(tur by q.u)
    |=  [path k=lobe]
    (lobe-to-blob k)
  ::
  ::  actual merge
  ::
```

XX document

###++reduce

``````

XX document

###++future

``````

XX document

###++add

``````

XX document

###++find

``````

XX document

###++clean

```
  ++  clean                                          ::  clean
    |=  wig=(urge)
    ^-  (urge)
    ?~  wig  ~
    ?~  t.wig  wig
    ?:  ?=(%& -.i.wig)
      ?:  ?=(%& -.i.t.wig)
        $(wig [[%& (add p.i.wig p.i.t.wig)] t.t.wig])
      [i.wig $(wig t.wig)]
    ?:  ?=(%| -.i.t.wig)
      $(wig [[%| (welp p.i.wig p.i.t.wig) (welp q.i.wig q.i.t.wig)] t.t.wig])
    [i.wig $(wig t.wig)]
  ::
```

XX document

###++match

``````

XX document

###++annotate

```
  ++  annotate                                      ::  annotate conflict
    |=  [us=[ship desk] th=[ship desk] p=(list ,@t) q=(list ,@t) r=(list ,@t)]
    ^-  (list ,@t)
    %-  zing
    ^-  (list (list ,@t))
    %-  flop
    ^-  (list (list ,@t))
    :-  :_  ~
        %^  cat  3  '<<<<<<<<<<<<' 
        %^  cat  3  ' '
        %^  cat  3  `@t`(scot %p -.us)
        %^  cat  3  '/'
        +.us
    :-  p
    :-  ~['------------']
    :-  r
    :-  ~['++++++++++++']
    :-  q
    :-  :_  ~
        %^  cat  3  '>>>>>>>>>>>>' 
        %^  cat  3  ' '
        %^  cat  3  `@t`(scot %p -.th)
        %^  cat  3  '/'
        +.th
    ~
  ::
```

XX document

    :-  ~['++++++++++++']

###++match

``````

XX document

###++qeal

```
  ++  qeal                                          ::  merge p,q
    |*  [us=[ship desk] th=[ship desk] pat=path p=miso q=miso r=(list) con=?]
    ^-  miso                                        ::  in case of conflict
    ~|  %qeal-fail
    ?>  ?=(%mut -.p)
    ?>  ?=(%mut -.q)
    ?>  ?=(%c -.q.p.p)
    ?>  ?=(%c -.q.p.q)
    =+  s=(clean p.q.p.p)
    =+  t=(clean p.q.p.q)
    :-  %mut
    :-  %c  ::  todo is this p.p.p?
    :-  %c
    |-  ^-  (urge)
    ::?~  s  ?:  (qual t)  t
    ::       ~|  %qail-conflict  !!
    ::?~  t  ?:  (qual s)  s
    ::       ~|  %qail-conflict  !!
    ?~  s  t
    ?~  t  s
    ?-    -.i.s
        %&
      ?-    -.i.t
          %&
        ?:  =(p.i.s p.i.t)
          [i.s $(s t.s, t t.t, r (slag p.i.s r))]
        ?:  (gth p.i.s p.i.t)
          [i.t $(t t.t, p.i.s (sub p.i.s p.i.t), r (slag p.i.t r))]
        [i.s $(s t.s, p.i.t (sub p.i.t p.i.s), r (slag p.i.s r))]
          %|
        ?:  =(p.i.s (lent p.i.t))
          [i.t $(s t.s, t t.t, r (slag p.i.s r))]
        ?:  (gth p.i.s (lent p.i.t))
          :-  i.t 
          $(t t.t, p.i.s (sub p.i.s (lent p.i.t)), r (slag (lent p.i.t) r))
        ?.  con  ~|  %quil-conflict  !!           ::  conflict
        ~&  [%quil-conflict-soft pat]
        =+  mar=(match-conflict us th s t r)
        [[%| p.mar] $(s p.q.mar, t q.q.mar, r r.q.mar)]
      ==
        %|
      ?-    -.i.t
          %|
        ?.  con  ~|  %quil-conflict  !!
        ~&  [%quil-conflict-soft pat]
        =+  mar=(match-conflict us th s t r)
        [[%| p.mar] $(s p.q.mar, t q.q.mar, r r.q.mar)]
          %&
        ?:  =(p.i.t (lent p.i.s))
          [i.s $(s t.s, t t.t, r (slag p.i.t r))]
        ?:  (gth p.i.t (lent p.i.s))
          :-  i.s
          $(s t.s, p.i.t (sub p.i.t (lent p.i.s)), r (slag (lent p.i.s) r))
        ?.  con  ~|  %quil-conflict  !!
        ~&  [%quil-conflict-soft pat]
        =+  mar=(match-conflict us th s t r)
        [[%| p.mar] $(s p.q.mar, t q.q.mar, r r.q.mar)]
      ==
    ==
```

XX document

###++quil

```
  ++  quil                                          ::  merge p,q
    |=  $:  us=[ship desk]
            th=[ship desk]
            pat=path
            p=(unit miso)
            q=(unit miso)
            r=(unit (list))
            con=?
        ==
    ^-  (unit miso)
    ?~  p  q                                        ::  trivial
    ?~  q  p                                        ::  trivial
    ?-  -.u.p
      %ins  ?>  ?=(%ins -.u.q)
            ?.  con  !!
            %-  some
            :-  %ins
            %-  roly
            %-  annotate
            :-  us 
            :-  th
            :-  (lore ((hard ,@) p.u.p)) 
            :-  (lore ((hard ,@) p.u.q))
            ~
      %del  p
      %mut  ?>  ?=(%mut -.u.q)
            %-  some
            %^  qeal  us  th
            :^  pat  u.p  u.q                       ::  merge p,q
            :-  %-  need  r
            con
    ==
  ::
```

XX document

###++meld

```
  ++  meld                                          ::  merge p,q from r
    |=  [p=yaki q=yaki r=yaki con=? us=[ship desk] th=[ship desk]]
    ^-  (map path blob)
    =+  s=(diff-yakis r p)
    =+  t=(diff-yakis r q)
    =+  lut=(luth s t)
    %-  |=  res=(map path blob)                        ::  add old
        ^-  (map path blob)
        %-  ~(uni by res)
        %-  mo
        %+  turn  
          %+  skip  (~(tap by q.r) ~)                  ::  loop through old
          |=  [pat=path bar=lobe]  ^-  ?
          (~(has in lut) pat)                          ::  skip updated
        |=  [pat=path bar=lobe]  ^-  [path blob]
        [pat (lobe-to-blob bar)]                       ::  lookup objects
    %+  roll  (~(tap in (luth s t)) ~)
    |=  [pat=path res=(map path blob)]
    =+  ^=  v
        %-  need
        %^  quil  us  th
        :-  pat
        :+  (~(get by s) pat)
          (~(get by t) pat)
        :_  con
        %-  %-  lift  lore
        %-  %-  lift  %-  hard  ,@                     ::  for %c
        %-  %-  lift  lobe-to-noun
        %-  ~(get by q.r)
        pat
    ?-    -.v
        %del  res                                      ::  no longer exists
        %ins                                           ::  new file
      %+  ~(put by res)  pat 
      %+  make-direct  p.v  %c                         ::  TODO content type?
        %mut                                           ::  patch from r
      %+  ~(put by res)  pat
      %-  make-direct
      :_  %c
      %+  lump  p.v
      %-  lobe-to-noun
      %-  ~(got by q.r)  pat
    ==
  ::
  ::  merge types
  ::
```

XX document

###++mate

```
  ++  mate                                          ::  merge p,q
    |=  con=?                                       ::  %mate, %meld
    |=  [p=yaki q=yaki us=[ship desk] th=[ship desk]]
    ^-  (map path blob)
    =+  r=(~(tap in (find-merge-points p q)) ~)
    ?~  r
      ~|(%mate-no-ancestor !!)
    ?:  =(1 (lent r))
      (meld p q i.r con us th)
    ~|(%mate-criss-cross !!)
  ::
```

XX document

###++keep

```
  ++  keep                                          ::  %this
    |=  [p=yaki q=yaki [ship desk] [ship desk]]
    ^-  (map path blob)
    %+  roll  (~(tap by q.p) ~)
    |=  [[pat=path lob=lobe] zar=(map path blob)]
    ^-  (map path blob)
    (~(put by zar) pat (lobe-to-blob lob))
  ::
```

XX document

###++drop

```
  ++  drop                                          ::  %that
    |=  [p=yaki q=yaki r=[ship desk] s=[ship desk]]
    ^-  (map path blob)
    (keep q p r s)
  ::
```

XX document

###++forge

```
  ++  forge                                         ::  %forge
    |=  [p=yaki q=yaki s=[ship desk] t=[ship desk]]
    ^-  (map path blob)
    =+  r=(~(tap in (find-merge-points p q)) ~)
    ?~  r
      ~|(%forge-no-ancestor !!)
    %-  |=  [r=yaki lut=(map lobe blob) hat=(map tako yaki)]
        =.  lat  lut
        =.  hut  hat
        (meld p q r & s t)                          ::  fake merge
    %+  roll  t.r                                   ::  fake ancestor
    |=  [par=yaki [for=_i.r lut=_lat hat=_hut]]
    =.  lat  lut
    =+  ^=  far
        ^-  (map path lobe)
        %-  ~(tur by (forge par for s t))
        |=  [k=path v=blob]  (blob-to-lobe v)
    =+  u=(make-yaki [r.par r.for ~] far `@da`0)    ::  fake yaki
    :-  u
    :_  (~(put by hat) r.u u)
    =<  -
    %-  update-lat
    :_  ~
    %-  ~(tur by q.u)
    |=  [path k=lobe]
    (lobe-to-blob k)
  ::
  ::  actual merge
  ::
```

XX document

###++merge

```
  ++  merge
    |=  [us=[ship desk] th=[ship desk]]
    |=  [p=yaki q=yaki r=@da s=$+([yaki yaki [ship desk] [ship desk]] (map path blob))]
    ^-  [yaki (map path blob)]
    =+  u=(s p q us th)
    =+  ^=  t
        ^-  (map path lobe)
        %+  roll  (~(tap by u) ~)
        |=  [[pat=path bar=blob] yeb=(map path lobe)]
        (~(put by yeb) pat (blob-to-lobe bar))
    :_  u
    (make-yaki [r.p r.q ~] t r)
  ::
```

XX document

###++strategy

```
  ++  strategy                                          ::  merge strategy
    |=  gem=?(%meld %mate %that %this)
    ?-  gem
      %meld  (mate %.y)
      %mate  (mate %.n)
      %this  keep
      %that  drop
    ==
  ::
```

XX document

###++construct

``````

XX document

###++read

```
  ++  read                                              ::    read:ze
    |=  mun=mood                                        ::  read at point
    ^-  (unit)
    ?:  ?=(%v p.mun)
      [~ `dome`+<+<.read]
    ?:  &(?=(%w p.mun) !?=(%ud -.q.mun))
      ?^(r.mun ~ [~ let])
    ?:  ?=(%w p.mun)
      =+  ^=  yak
          %-  aeon-to-yaki
          let
      ?^(r.mun ~ [~ [t.yak (forge-nori yak)]])
      ::?>  ?=(^ hit)  ?^(r.mun ~ [~ i.hit])     ::  what do?? need [@da nori]
    (query(ank ank:(descend-path:(zu ank) r.mun)) p.mun)
  ::
```

XX document

###++read

```
  ++  read                                              ::    read:ze
    |=  mun=mood                                        ::  read at point
    ^-  (unit)
    ?:  ?=(%v p.mun)
      [~ `dome`+<+<.read]
    ?:  &(?=(%w p.mun) !?=(%ud -.q.mun))
      ?^(r.mun ~ [~ let])
    ?:  ?=(%w p.mun)
      =+  ^=  yak
          %-  aeon-to-yaki
          let
      ?^(r.mun ~ [~ [t.yak (forge-nori yak)]])
      ::?>  ?=(^ hit)  ?^(r.mun ~ [~ i.hit])     ::  what do?? need [@da nori]
    (query(ank ank:(descend-path:(zu ank) r.mun)) p.mun)
  ::
```

XX document

###++equiv

```
  ++  equiv                                             ::  test paths
    |=  [p=(map path lobe) q=(map path lobe)]
    ^-  ?
    =-  ?.  qat  %.n
        %+  levy  (~(tap by q) ~)
        |=  [pat=path lob=lobe]
        (~(has by p) pat)
    ^=  qat
    %+  levy  (~(tap by p) ~)
    |=  [pat=path lob=lobe]
    =+  zat=(~(get by q) pat)
    ?~  zat  %.n
    =((lobe-to-noun u.zat) (lobe-to-noun lob))
  ::
```

XX document

###++edit

```
  ++  edit                                              ::    edit:ze
    |=  [wen=@da lem=nori]                              ::  edit
    ^+  +>
    ?-  -.lem
      &  =^  yak  lat                                   ::  merge objects
             %+  forge-yaki  wen
             ?:  =(let 0)                               ::  initial import
               [~ q.lem]
             [(some r:(aeon-to-yaki let)) q.lem]
         ?.  ?|  =(0 let)
                 !=((lent p.yak) 1)
                 !(equiv q.yak q:(aeon-to-yaki let))
             ==
           +>.$                                         ::  silently ignore
         =:  let  +(let)
             hit  (~(put by hit) +(let) r.yak)
             hut  (~(put by hut) r.yak yak)
         ==
         +>.$(ank (checkout-ankh q.yak))
      |  +>.$(lab ?<((~(has by lab) p.lem) (~(put by lab) p.lem let)))
    ==
::
```

XX document

###++zu

```
++  zu                                                  ::  filesystem
  |=  ank=ankh                                          ::  filesystem state
  =|  myz=(list ,[p=path q=miso])                       ::  changes in reverse
  =|  ram=path                                          ::  reverse path into
  |%
```

XX document

###++rehash

```
  ++  rehash                                            ::  local rehash
    ^-  cash
    %+  mix  ?~(q.ank 0 p.u.q.ank)
    =+  axe=1
    |-  ^-  cash
    ?~  r.ank  _@
    ;:  mix
      (shaf %dash (mix axe (shaf %dush (mix p.n.r.ank p.q.n.r.ank))))
      $(r.ank l.r.ank, axe (peg axe 2))
      $(r.ank r.r.ank, axe (peg axe 3))
    ==
  ::
```

XX document

###++update

``````

XX document

###++ascend

```
  ++  ascend                                            ::  ascend
    |=  [lol=@ta kan=ankh]
    ^+  +>
    ?>  &(?=(^ ram) =(lol i.ram))
    %=    +>
        ram  t.ram
        ank
      ?:  =([0 ~ ~] ank)
        ?.  (~(has by r.kan) lol)  kan
        kan(r (~(del by r.kan) lol))
      kan(r (~(put by r.kan) lol ank))
    ==
  ::
```

XX document

###++push

``````

XX document

###++descend

```
  ++  descend                                           ::  descend
    |=  lol=@ta
    ^+  +>
    =+  you=(~(get by r.ank) lol)
    +>.$(ram [lol ram], ank ?~(you [*cash ~ ~] u.you))
  ::
```

XX document

###++descend

```
  ++  descend                                           ::  descend
    |=  lol=@ta
    ^+  +>
    =+  you=(~(get by r.ank) lol)
    +>.$(ram [lol ram], ank ?~(you [*cash ~ ~] u.you))
  ::
```

XX document

###++overwrite

```
  ++  overwrite                                         ::  write over
    |=  [pum=umph val=(unit ,[p=cash q=*])]
    ^+  +>
    ?~  q.ank
      ?~  val  +>
      (push-change %ins q.u.val)
    ?~  val
      (push-change %del q.u.q.ank)
    ?:  =(q.u.val q.u.q.ank)  +>
    (push-change %mut ((diff pum) q.u.q.ank q.u.val))
  ::
```

XX document

###++change

``````

XX document

###++rm

``````

XX document

###++drum

```
  ++  drum                                              ::  apply effect
    |=  [pax=path mis=miso]                             ::  XX unused (++dune)
    ^+  +>
    ?^  pax
      update-hash:(ascend:$(pax t.pax, +> (descend i.pax)) i.pax ank)
    ~|  %clay-fail
    ?-    -.mis
        %del
      ?>  &(?=(^ q.ank) =(q.u.q.ank p.mis))
      +>.$(p.ank (mix p.u.q.ank p.ank), q.ank ~)
    ::
        %ins
      ?>  ?=(~ q.ank)
      =+  sam=(sham p.mis)
      +>.$(p.ank (mix sam p.ank), q.ank [~ sam p.mis])
    ::
        %mut
      ?>  ?=(^ q.ank)
      =+  nex=(lump p.mis q.u.q.ank)
      =+  sam=(sham nex)
      +>.$(p.ank :(mix sam p.u.q.ank p.ank), q.ank [~ sam nex])
    ==
  ::
```

XX document

    |=  [pax=path mis=miso]                             ::  XX unused (++dune)

###++dune

```
  ++  dune                                              ::  apply
    |-  ^+  +                                           ::  XX unused (++durn)
    ?~  myz  +
    =>  .(+ (drum p.i.myz q.i.myz))
    $(myz ?>(?=(^ myz) t.myz))
  ::
```

XX document

    |-  ^+  +                                           ::  XX unused (++durn)

###++durn

```
  ++  durn                                              ::  apply forward
    |=  nyp=soba                                        ::  XX unused
    ^+  +>
    ?:  =([0 0] p.nyp)
      dune(myz q.nyp)
    =>  ?:  =(p.ank p.p.nyp)  .
        ~&  [%durn-in-wrong p.ank p.p.nyp]
        .
    =.  +>  dune(myz q.nyp)
    =>  ?:  =(p.ank q.p.nyp)  .
        ~&  [%durn-out-wrong p.ank q.p.nyp]
        .
    +>
```

XX document
