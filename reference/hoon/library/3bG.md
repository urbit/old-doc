##section 3bG, URL handling

###++deft

```
++  deft                                                ::  import url path
  |=  rax=(list ,@t)
  |-  ^-  pork
  ?~  rax
    [~ ~]
  ?~  t.rax
    =+  den=(trip i.rax)
    =+  ^=  vex
      %-  %-  full
          ;~(plug sym ;~(pose (stag ~ ;~(pfix dot sym)) (easy ~)))
      [[1 1] (trip i.rax)]
    ?~  q.vex
      [~ [i.rax ~]]
    [+.p.u.q.vex [-.p.u.q.vex ~]]
  =+  pok=$(rax t.rax)
  :-  p.pok
  [i.rax q.pok]
::
```

XX document

###++fest

```
++  fest                                                ::  web synthesizer
  |=  [hom=path raw=path]
  |*  yax=$+(epic *)
  (yax (fuel (fain hom raw)))
::
```

XX document

###++folk

```
++  folk                                                ::  silk construction
  |=  [hom=path raw=path]
  |*  yox=$+((pair beam path) *)
  (yox (fain hom raw))
::
```

XX document

###++fuel

```
++  fuel                                                ::  parse fcgi
  |=  [bem=beam but=path]
  ^-  epic
  ?>  ?=([%web @ *] but)
  =+  dyb=(slay i.t.but)
  ?>  ?&  ?=([~ %many *] dyb)
          ?=([* * *] p.u.dyb)
          ::  ?=([%$ %tas *] i.p.u.dyb)
          ?=([%many *] i.p.u.dyb)
          ?=([%blob *] i.t.p.u.dyb)
      ==
  =+  ced=((hard cred) p.i.t.p.u.dyb)
  ::  =+  nep=q.p.i.p.u.dyb
  =+  ^=  nyp  ^-  path
      %+  turn  p.i.p.u.dyb
      |=  a=coin  ^-  @ta
      ?>  ?=([%$ %ta @] a)
      ?>(((sane %ta) q.p.a) q.p.a)
  =+  ^=  gut  ^-  (list ,@t)
      %+  turn  t.t.p.u.dyb
      |=  a=coin  ^-  @t
      ?>  ?=([%$ %t @] a)
      ?>(((sane %t) q.p.a) q.p.a)
  =+  ^=  quy
      |-  ^-  (list ,[p=@t q=@t])
      ?~  gut  ~
      ?>  ?=(^ t.gut)
      [[i.gut i.t.gut] $(gut t.t.gut)]
  :*  (~(gas by *(map cord cord)) quy)
      ced
      bem
      t.t.but
      nyp
  ==
::
```

XX document

###++gist

```
++  gist                                                ::  convenient html
  |=  [hom=path raw=path]
  |=  yax=$+(epic marl)
  %-  (fest hom raw)
  |=  piq=epic
  ^-  manx
  =+  ^=  sip                                           ::  skip blanks
      |=  mal=marl
      ?~(mal ~ ?.(|(=(:/(~) i.mal) =(:/([10 ~]) i.mal)) mal $(mal t.mal)))
  =+  zay=`marl`(yax piq)
  =.  zay  (sip zay)
  =+  ^=  twa
      |-  ^-  [p=marl q=marl]
      ?~  zay  [~ ~]
      ?:  ?=([[[%head *] *] *] zay)
        [c.i.zay ?:(?=([[[%body *] *] ~] t.zay) c.i.t.zay t.zay)]
      ?:  ?=([[[%title *] *] *] zay)
        [[i.zay ~] t.zay]
      [~ zay]
  [/html [/head (sip p.twa)] [/body (sip q.twa)] ~]
::
```

XX document

###++sifo

```
++  sifo                                                ::  64-bit encode
  |=  tig=@
  ^-  tape
  =+  poc=(~(dif fo 3) 0 (met 3 tig))
  =+  pad=(lsh 3 poc (swap 3 tig))
  =+  ^=  cha
  'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
  =+  ^=  sif
      %-  flop
      |-  ^-  tape
      ?~  pad
        ~
      =+  d=(end 0 6 pad)
      [(cut 3 [0 d] cha) $(pad (rsh 0 6 pad))]
  (weld (scag (sub (lent sif) poc) sif) (trip (fil 3 poc '=')))
::
```

XX document

###++urle

```
++  urle                                                ::  URL encode
  |=  tep=tape
  ^-  tape
  %-  zing
  %+  turn  tep
  |=  tap=char
  =+  xen=|=(tig=@ ?:((gte tig 10) (add tig 55) (add tig '0')))
  ?:  ?|  &((gte tap 'a') (lte tap 'z'))
          &((gte tap 'A') (lte tap 'Z'))
          &((gte tap '0') (lte tap '9'))
          =('.' tap)
          =('-' tap)
          =('~' tap)
          =('_' tap)
      ==
    [tap ~]
  ['%' (xen (rsh 0 4 tap)) (xen (end 0 4 tap)) ~]
::
```

XX document

###++urld

```
++  urld                                                ::  URL decode
  |=  tep=tape
  ^-  (unit tape)
  ?~  tep  [~ ~]
  ?:  =('%' i.tep)
    ?.  ?=([@ @ *] t.tep)  ~
    =+  nag=(mix i.t.tep (lsh 3 1 i.t.t.tep))
    =+  val=(rush nag hex:ag)
    ?~  val  ~
    =+  nex=$(tep t.t.t.tep)
    ?~(nex ~ [~ [`@`u.val u.nex]])
  =+  nex=$(tep t.tep)
  ?~(nex ~ [~ i.tep u.nex])
::
```

XX document

###++earl

```
++  earl                                                ::  local purl to tape
  |=  [who=@p pul=purl]
  ^-  purl
  pul(q.q [(rsh 3 1 (scot %p who)) q.q.pul])
::
```

XX document

###++earn

```
++  earn                                                ::  purl to tape
  |=  pul=purl
  ^-  tape
  =<  apex
  |%
```

XX document

###++apex
  
```
  ++  apex
    ^-  tape
    :(weld head "/" body tail)
  ::
```

XX document

###++body
  
```
  ++  body
    |-  ^-  tape
    ?~  q.q.pul
      ?~(p.q.pul ~ ['.' (trip u.p.q.pul)])
    =+  seg=(trip i.q.q.pul)
    ?:(=(~ t.q.q.pul) seg (weld seg `tape`['/' $(q.q.pul t.q.q.pul)]))
  ::
```

XX document

###++head
  
```
  ++  head
    ^-  tape
    ;:  weld
      ?:(&(p.p.pul !=([& /localhost] r.p.pul)) "https://" "http://")
    ::
      ?-  -.r.p.pul
        |  (trip (rsh 3 1 (scot %if p.r.p.pul)))
        &  =+  rit=(flop p.r.p.pul)
           |-  ^-  tape
           ?~(rit ~ (weld (trip i.rit) ?~(t.rit "" `tape`['.' $(rit t.rit)])))
      ==
    ::
      ?~(q.p.pul ~ `tape`[':' (trip (rsh 3 2 (scot %ui u.q.p.pul)))])
    ==
  ::
```

XX document

###++tail
  
```
  ++  tail
    ^-  tape
    ?:  =(~ r.pul)  ~
    :-  '?'
    |-  ^-  tape
    ?~  r.pul  ~
    ;:  weld
      (trip p.i.r.pul)
      "="
      (trip q.i.r.pul)
      ?~(t.r.pul ~ `tape`['&' $(r.pul t.r.pul)])
    ==
  --
::
```

XX document

###++epur

```
++  epur                                                ::  url/header parser
  =<  |=(a=cord (rush a apex))
  |%
```

XX document

###++apat
  
```
  ++  apat                                              ::  2396 abs_path
    %+  cook  deft
    (ifix [fas ;~(pose fas (easy ~))] (more fas smeg))
```

XX document

###++apex
  
```
  ++  apex  auri
```

XX document

###++auri
  
```
  ++  auri
    %+  cook
      |=  a=purl
      ?.(=([& /localhost] r.p.a) a a(p.p &))
    ;~  plug
      ;~  plug
        %+  sear
          |=  a=@t
          ^-  (unit ,?)
          ?+(a ~ %http [~ %|], %https [~ %&])
        ;~(sfix scem ;~(plug col fas fas))
        thor
      ==
      ;~(plug ;~(pose apat (easy *pork)) yque)
    ==
```

XX document

###++cock
  
```
  ++  cock                                              ::  cookie
    (most ;~(plug sem ace) ;~(plug toke ;~(pfix tis tosk)))
```

XX document

###++dlab
  
```
  ++  dlab                                              ::  2396 domainlabel
    %+  sear
      |=  a=@ta
      ?.(=('-' (rsh 3 (dec (met 3 a)) a)) [~ u=a] ~)
    %+  cook  cass
    ;~(plug aln (star alp))
  ::
```

XX document

###++fque
  
```
  ++  fque  (cook crip (plus pquo))                     ::  normal query field
```

XX document

###++fquu
  
```
  ++  fquu  (cook crip (star pquo))                     ::  optional field
```

XX document

###++pcar
  
```
  ++  pcar  ;~(pose pure pesc psub col pat)             ::  2396 path char
```

XX document

###++pcok
  
```
  ++  pcok  ;~  pose                                    ::  cookie char
              (just `@`0x21)
              (shim 0x23 0x2b)
              (shim 0x2d 0x3a)
              (shim 0x3c 0x5b)
              (shim 0x5d 0x7e)
            ==
```

XX document

###++pesc
  
```
  ++  pesc  ;~(pfix cen mes)                            ::  2396 escaped
```

XX document

###++pold
  
```
  ++  pold  (cold ' ' (just '+'))                       ::  old space code
```

XX document

###++pque
  
```
  ++  pque  ;~(pose pcar fas wut)                       ::  3986 query char
```

XX document

###++pquo
  
```
  ++  pquo  ;~(pose pure pesc pold)                     ::  normal query char
```

XX document

###++pure
  
```
  ++  pure  ;~(pose aln hep dot cab sig)                ::  2396 unreserved
```

XX document

###++psub
  
```
  ++  psub  ;~  pose                                    ::  3986 sub-delims
              zap  buc  pam  soq  pel  per
              tar  lus  com  sem  tis
            ==
```

XX document

###++ptok
  
```
  ++  ptok  ;~  pose                                    ::  2616 token
              aln  zap  hax  buc  cen  pam  soq  tar  lus
              hep  dot  ket  cab  tec  bar  sig
            ==
```

XX document

###++scem
  
```
  ++  scem                                              ::  2396 scheme
    %+  cook  cass
    ;~(plug alf (star ;~(pose aln lus hep dot)))
  ::
```

XX document

###++smeg
  
```
  ++  smeg  (cook crip (plus pcar))                     ::  2396 segment
```

XX document

###++tock
  
```
  ++  tock  (cook crip (plus pcok))                     ::  6265 cookie-value
```

XX document

###++tosk
  
```
  ++  tosk  ;~(pose tock (ifix [doq doq] tock))         ::  6265 cookie-value
```

XX document

###++toke
  
```
  ++  toke  (cook crip (plus ptok))                     ::  2616 token
```

XX document

###++thor
  
```
  ++  thor                                              ::  2396 host/port
    %+  cook  |*(a=[* *] [+.a -.a])
    ;~  plug
      thos
      ;~(pose (stag ~ ;~(pfix col dim:ag)) (easy ~))
    ==
```

XX document

###++thos
  
```
  ++  thos                                              ::  2396 host, no local
    ;~  plug
      ;~  pose
        %+  stag  %&
        %+  sear                                        ::  LL parser weak here
          |=  a=(list ,@t)
          =+  b=(flop a)
          ?>  ?=(^ b)
          =+  c=(end 3 1 i.b)
          ?.(&((gte c 'a') (lte c 'z')) ~ [~ u=b])
        (most dot dlab)
      ::
        %+  stag  %|
        =+  tod=(ape:ag ted:ab)
        %+  bass  256
        ;~(plug tod (stun [3 3] ;~(pfix dot tod)))
      ==
    ==
```

XX document

###++yque
  
```
  ++  yque                                              ::  query ending
    ;~  pose
      ;~(pfix wut yquy)
      (easy ~)
    ==
```

XX document

###++yquy
  
```
  ++  yquy                                              ::  query
    ;~  pose                                            ::  proper query
      %+  more
        ;~(pose pam sem)
      ;~(plug fque ;~(pose ;~(pfix tis fquu) (easy '')))
    ::
      %+  cook                                          ::  funky query
        |=(a=tape [[%$ (crip a)] ~])
      (star pque)
    ==
```

XX document

###++zest
  
```
  ++  zest                                              ::  2616 request-uri
    ;~  pose
      (stag %& (cook |=(a=purl a) auri))
      (stag %| ;~(plug apat yque))
    ==
  --
```

XX document
