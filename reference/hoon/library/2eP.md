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
###++diff 
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
##  ++  abet
##  ++  hink
##  ++  lonk
##  ++  lune
##  ++  merg
##  ++  main
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
###++lore  
###++role  

``````
###++lump  
###++lure  

```
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
###++limp  
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
###++husk  
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
###++lusk  
##  ++  abet
##  ++  done
##  ++  main
###++nude   

```
++  nude                                                ::  tree change
  |=  [a=* b=*]
  ^-  [p=upas q=upas]
  =<  [p=(tred a b) q=(tred b a)]
  |%
```
##  ++  axes 
##  ++  tred 

---

