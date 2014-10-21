##section 2eP, diff          **noted as "(move me)" in source**
---

###++berk 

```
++  berk                                                ::  invert diff patch
  |*  bur=(urge)
  |-  ^+  bur
  ?~  bur  ~
  :_  $(bur t.bur)
  ?-  -.i.bur
    &  i.bur
    |  [%| q.i.bur p.i.bur]
  ==
::
```

XX document

###++diff 

```
++  diff                                                ::  generate patch
  |=  pum=umph
  |=  [old=* new=*]  ^-  udon
  :-  pum
  ?+  pum  ~|(%unsupported !!)
    %a  [%d (nude old new)]
    %b  =+  [hel=(cue ((hard ,@) old)) hev=(cue ((hard ,@) new))]
        [%d (nude hel hev)]
    %c  =+  [hel=(lore ((hard ,@) old)) hev=(lore ((hard ,@) new))]
        [%c (lusk hel hev (loss hel hev))]
  ==
::
```

XX document

###++loss 

```
++  loss                                                ::  longest subsequence
  ~/  %loss
  |*  [hel=(list) hev=(list)]
  |-  ^+  hev
  =+  ^=  sev
      =+  [inx=0 sev=*(map ,@t (list ,@ud))]
      |-  ^+  sev
      ?~  hev  sev
      =+  guy=(~(get by sev) i.hev)
      $(hev t.hev, inx +(inx), sev (~(put by sev) i.hev [inx ?~(guy ~ u.guy)]))
  =|  gox=[p=@ud q=(map ,@ud ,[p=@ud q=_hev])]
  =<  abet
  =<  main
  |%
```

XX document

###++abet

```
  ++  abet  =.(q.rag ?:(=([& 0] p.rag) q.rag [p.rag q.rag]) (flop q.rag))
```

XX document

###++hink

```
  ++  hink                                              ::  extend fits top
    |=  [inx=@ud goy=@ud]  ^-  ?
    |(=(p.gox inx) (lth goy p:(need (~(get by q.gox) inx))))
  ::
```

XX document

###++lonk

```
  ++  lonk                                              ::  extend fits bottom
    |=  [inx=@ud goy=@ud]  ^-  ?
    |(=(0 inx) (gth goy p:(need (~(get by q.gox) (dec inx)))))
  ::
```

XX document

###++lune

```
  ++  lune                                              ::  extend
    |=  [inx=@ud goy=@ud]
    ^+  +>
    %_    +>.$
        gox
      :-  ?:(=(inx p.gox) +(p.gox) p.gox)
      %+  ~(put by q.gox)  inx
      [goy (snag goy hev) ?:(=(0 inx) ~ q:(need (~(get by q.gox) (dec inx))))]
    ==
  ::
```

XX document

###++merg

```
  ++  merg                                              ::  merge all matches
    |=  gay=(list ,@ud)
    ^+  +>
    =+  ^=  zes
        =+  [inx=0 zes=*(list ,[p=@ud q=@ud])]
        |-  ^+  zes
        ?:  |(?=(~ gay) (gth inx p.gox))  zes
        ?.  (lonk inx i.gay)  $(gay t.gay)
        ?.  (hink inx i.gay)  $(inx +(inx))
        $(inx +(inx), gay t.gay, zes [[inx i.gay] zes])
    |-  ^+  +>.^$
    ?~(zes +>.^$ $(zes t.zes, +>.^$ (lune i.zes)))
  ::
```

XX document

###++main

```
  ++  main
    |-  ^+  +
    ?~  hel
      ?~  hev
        ?>(?=(~ lcs) +)
      $(hev t.hev, rag (done %| ~ [i.hev ~]))
    ?~  hev
      $(hel t.hel, rag (done %| [i.hel ~] ~))
    ?~  lcs
      +(rag (done %| (flop hel) (flop hev)))
    ?:  =(i.hel i.lcs)
      ?:  =(i.hev i.lcs)
        $(lcs t.lcs, hel t.hel, hev t.hev, rag (done %& 1))
      $(hev t.hev, rag (done %| ~ [i.hev ~]))
    ?:  =(i.hev i.lcs)
      $(hel t.hel, rag (done %| [i.hel ~] ~))
    $(hel t.hel, hev t.hev, rag (done %| [i.hel ~] [i.hev ~]))
  --
```

XX document

###++locz  

```
++  locz                                                ::  trivial algorithm
  |=  [hel=tape hev=tape]
  ^-  tape
  =+  [leh=(lent hel) veh=(lent hev)]
  =-  (flop q.yun)
  ^=  yun
  |-  ^-  [p=@ud q=tape]
  ~+
  ?:  |(=(0 leh) =(0 veh))  [0 ~]
  =+  [dis=(snag (dec leh) hel) dat=(snag (dec veh) hev)]
  ?:  =(dis dat)
    =+  say=$(leh (dec leh), veh (dec veh))
    [+(p.say) [dis q.say]]
  =+  [lef=$(leh (dec leh)) rig=$(veh (dec veh))]
  ?:((gth p.lef p.rig) lef rig)
::
```

XX document

###++lore  

```
++  lore                                                ::  atom to line list
  ~/  %lore
  |=  lub=@
  =|  tez=(list ,@t)
  |-  ^+  tez
  ?:  =(0 lub)  (flop tez)
  =+  ^=  meg
      =+  meg=0
      |-  ^-  @ud
      =+  gam=(cut 3 [meg 1] lub)
      ?:(|(=(10 gam) =(0 gam)) meg $(meg +(meg)))
  =+  res=(rsh 3 +(meg) lub)
  ?:  &(=(0 (cut 3 [meg 1] lub)) !=(0 res))
    !!
  $(lub res, tez [(end 3 meg lub) tez])
::
```

XX document

###++role  

``````

++  lure                                                ::  apply tree diff
  |=  [a=* b=upas]
  ^-  *
  ?^  -.b
    [$(b -.b) $(b +.b)]
  ?+  -.b  ~|(%unsupported !!)
    %0  .*(a [0 p.b])
    %1  .*(a [1 p.b])
  ==
```

XX document

###++limp  

```
++  limp                                                ::  invert patch
  |=  don=udon  ^-  udon
  :-  p.don
  ?+  -.q.don  ~|(%unsupported !!)
    %a  [%a q.q.don p.q.don]
    %c  [%c (berk p.q.don)]
    %d  [%d q.q.don p.q.don]
  ==
::
```

XX document

###++hump  

```
++  hump                                                ::  general prepatch
  |=  [pum=umph src=*]  ^-  *
  ?+  pum  ~|(%unsupported !!)
    %a  src
    %b  (cue ((hard ,@) src))
    %c  (lore ((hard ,@) src))
  ==
::
```

XX document

###++husk  

```
++  husk                                                ::  unprepatch
  |=  [pum=umph dst=*]  ^-  *
  ?+  pum  ~|(%unsupported !!)
    %a  dst
    %b  (jam dst)
    %c  (roly ((hard (list ,@)) dst))
  ==
::
```

XX document

###++lurk  

```
++  lurk                                                ::  apply list patch
  |*  [hel=(list) rug=(urge)]
  ^+  hel
  =+  war=`_hel`~
  |-  ^+  hel
  ?~  rug  (flop war)
  ?-    -.i.rug
      &
    %=   $
      rug  t.rug
      hel  (slag p.i.rug hel)
      war  (weld (flop (scag p.i.rug hel)) war)
    ==
  ::
      |
    %=  $
      rug  t.rug
      hel  =+  gur=(flop p.i.rug)
           |-  ^+  hel
           ?~  gur  hel
           ?>(&(?=(^ hel) =(i.gur i.hel)) $(hel t.hel, gur t.gur))
      war  (weld q.i.rug war)
    ==
  ==
::
```

XX document

###++lusk  

```
++  lusk                                                ::  lcs to list patch
  |*  [hel=(list) hev=(list) lcs=(list)]
  =+  ^=  rag
      ^-  $%  [& p=@ud]
              [| p=_lcs q=_lcs]
          ==
      [%& 0]
  =>  .(rag [p=rag q=*(list ,_rag)])
  =<  abet  =<  main
  |%
```

XX document

###++abet

```
  ++  abet  =.(q.rag ?:(=([& 0] p.rag) q.rag [p.rag q.rag]) (flop q.rag))
```

XX document

###++done

```
  ++  done
    |=  new=_p.rag
    ^+  rag
    ?-  -.p.rag
      |   ?-  -.new
            |  [[%| (weld p.new p.p.rag) (weld q.new q.p.rag)] q.rag]
            &  [new [p.rag q.rag]]
          ==
      &   ?-  -.new
            |  [new ?:(=(0 p.p.rag) q.rag [p.rag q.rag])]
            &  [[%& (add p.p.rag p.new)] q.rag]
          ==
    ==
  ::
```

XX document

###++main

```
  ++  main
    |-  ^+  +
    ?~  hel
      ?~  hev
        ?>(?=(~ lcs) +)
      $(hev t.hev, rag (done %| ~ [i.hev ~]))
    ?~  hev
      $(hel t.hel, rag (done %| [i.hel ~] ~))
    ?~  lcs
      +(rag (done %| (flop hel) (flop hev)))
    ?:  =(i.hel i.lcs)
      ?:  =(i.hev i.lcs)
        $(lcs t.lcs, hel t.hel, hev t.hev, rag (done %& 1))
      $(hev t.hev, rag (done %| ~ [i.hev ~]))
    ?:  =(i.hev i.lcs)
      $(hel t.hel, rag (done %| [i.hel ~] ~))
    $(hel t.hel, hev t.hev, rag (done %| [i.hel ~] [i.hev ~]))
  --
```

XX document

###++nude   

```
++  nude                                                ::  tree change
  |=  [a=* b=*]
  ^-  [p=upas q=upas]
  =<  [p=(tred a b) q=(tred b a)]
  |%
```

XX document

###++axes

```
  ++  axes                                              ::  locs of nouns
    |=  [a=@ b=*]  ^-  (map ,* axis)
    =+  c=*(map ,* axis)
    |-  ^-  (map ,* axis)
    =>  .(c (~(put by c) b a))
    ?@  b
      c
    %-  ~(uni by c)
    %-  ~(uni by $(a (mul 2 a), b -.b))
    $(a +((mul 2 a)), b +.b)
  ::
```

XX document

###++tred

```
  ++  tred                                              ::  diff a->b
    |=  [a=* b=*]  ^-  upas
    =|  c=(unit ,*)
    =+  d=(axes 1 a)
    |-  ^-  upas
    =>  .(c (~(get by d) b))
    ?~  c
      ?@  b
        [%1 b]
      =+  e=^-(upas [$(b -.b) $(b +.b)])
      ?-  e
        [[%1 *] [%1 *]]  [%1 [p.p.e p.q.e]]
        *  e
      ==
    [%0 u.c]
  --
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
```

---
