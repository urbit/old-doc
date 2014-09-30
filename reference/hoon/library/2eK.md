section 2eK, formatting (layout)      

###++re

```
++  re
  |_  tac=tank
```
  
###++ram

###++win

```
  ++  win
    |=  [tab=@ edg=@]
    =+  lug=`wall`~
    |^  |-  ^-  wall
        ?-    -.tac
            %leaf  (rig p.tac)
            %palm
          ?:  fit
            (rig ram)
          ?~  q.tac
            (rig q.p.tac)
          ?~  t.q.tac
            (rig(tab (add 2 tab), lug $(tac i.q.tac)) q.p.tac)
          =>  .(q.tac `(list tank)`q.tac)
          =+  lyn=(mul 2 (lent q.tac))
          =+  ^=  qyr
              |-  ^-  wall
              ?~  q.tac
                lug
              %=  ^$
                tac  i.q.tac
                tab  (add tab (sub lyn 2))
                lug  $(q.tac t.q.tac, lyn (sub lyn 2))
              ==
          (wig(lug qyr) q.p.tac)
        ::
            %rose
          ?:  fit
            (rig ram)
          =+  ^=  gyl
            |-  ^-  wall
            ?~  q.tac
              ?:(=(%$ r.p.tac) lug (rig r.p.tac))
            ^$(tac i.q.tac, lug $(q.tac t.q.tac), tab din)
          ?:  =(%$ q.p.tac)
            gyl
          (wig(lug gyl) q.p.tac)
        ==
    ::
```

###++din 

###++fit 

```
    ++  fit  (lte (lent ram) (sub edg tab))
```

###++rig

###++wig

```
    ++  wig
      |=  hom=tape
      ^-  wall
      ?~  lug
        (rig hom)
      =+  lin=(lent hom)
      =+  wug=:(add 1 tab lin)
      ?.  =+  mir=i.lug
          |-  ?~  mir
                |
              ?|(=(0 wug) ?&(=(' ' i.mir) $(mir t.mir, wug (dec wug))))
        (rig hom)       :: ^ XX regular form?
      [(runt [tab ' '] (weld hom `tape`[' ' (slag wug i.lug)])) t.lug]
    --
  --
```


