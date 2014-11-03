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

Parse extension from last element of url

    ~zod/try=> (deft /foo/bar/'baz.txt')
    [p=[~ ~.txt] q=<|foo bar baz|>]
    ~zod/try=> (deft /foo/bar/baz)
    [p=~ q=<|foo bar baz|>]

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

Split concrete spur out of full path, producing location beam and remainder path

    ~zod/try=> (fain / %)
    [p=[[p=~zod q=%try r=[%da p=~2014.11.1..00.07.17..c835]] s=/] q=/]
    ~zod/try=> (fain /lok %)
    ! exit
    ~zod/try=> (fain / %/mer/lok/tem)
    [ p=[[p=~zod q=%try r=[%da p=~2014.11.1..00.08.03..bfdf]] s=/] 
      q=/tem/lok/mer
    ]
    ~zod/try=> (fain /mer %/mer/lok/tem)
    [p=[[p=~zod q=%try r=[%da p=~2014.11.1..00.08.15..4da0]] s=/mer] q=/tem/lok]
    ~zod/try=> (fain /lok/mer %/mer/lok/tem)
    [p=[[p=~zod q=%try r=[%da p=~2014.11.1..00.08.24..4d9e]] s=/lok/mer] q=/tem]
    ~zod/try=> (fain /lok/mer %/mer)
    ! exit
    ~zod/try=> (fain /hook/hymn/tor %/tor/hymn/hook/'._req_1234__')
    [ p=[[p=~zod q=%try r=[%da p=~2014.11.1..00.09.25..c321]] s=/hook/hymn/tor]
      q=/._req_1234__
    ]


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

Retrieieve %унку fcgi, used primarily in /hook files.

See %ащкв doc.

```
~zod/main=> (fuel [[p=~zod q=%try r=[%ud p=2]] s=/psal] /web/'._.~-~~~~.gen~-~-_~~05vg0001v09f0n30fbh7dn6ab2jakmmspdq04nef5h70qbd5lh6atr4c5j2qrbldpp62q1df1in0sr1ding0c3qgt7kclj74qb65lm6atrkc5k2qpr5e1mmispdchin4p3fegmiqrjpdlo62p1dchsn4p39comn8pbcehgmsbbef5p7crrifr3o035dhgfrk2b5__')
[ qix={}
    ced
  [ hut=[p=%.y q=[~ 8.445] r=[%.n p=.0.0.0.0]]
    aut={[p=%$ q={'~rovryn-natlet-fidryd-dapmyn--todred-simpeg-hatwel-firfet'}]}
    orx='laspex-harnum-fadweb-mipbyn'
    acl=[~ 'en-US,en;q=0.8']
    cip=[%.y p=.127.0.0.1]
    cum={}
  ]
  bem=[[p=~zod q=%try r=[%ud p=2]] s=/psal]
  but=/
  nyp=/gen
]
```

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
      |-  ^-  tape
      ?~  pad
        ~
      =+  d=(end 0 6 pad)
      [(cut 3 [d 1] cha) $(pad (rsh 0 6 pad))]
  (weld (flop (slag poc sif)) (trip (fil 3 poc '=')))
::
```

Encode atom to MIME base64

    ~zod/main=> (sifo 'foobar')
    "Zm9vYmFy"
    ~zod/main=> (sifo 1)
    "Q=="
    ~zod/main=> (sifo (shax %hi))
    "j0NDRmSPa5bfid2pAcUXaxCm2Dlh3TwayItZstwyeqQ="


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

URL escape tape

    ~zod/main=> (urle "hello")
    "hello"
    ~zod/main=> (urle "hello dear")
    "hello%20dear"
    ~zod/main=> (urle "hello-my?=me  !")
    "hello-my%3F%3Dme%20%20%21"


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

Parse URL escaped tape

    ~zod/main=> (urld "hello")
    [~ "hello"]
    ~zod/main=> (urld "hello%20dear")
    [~ "hello dear"]
    ~zod/main=> (urld "hello-my%3F%3Dme%20%20%21")
    [~ "hello-my?=me  !"]
    ~zod/main=> (urld "hello-my%3F%3Dme%20%2%21")
    ~

###++earl

```
++  earl                                                ::  localize purl
  |=  [who=@p pul=purl]
  ^-  purl
  pul(q.q [(rsh 3 1 (scot %p who)) q.q.pul])
::
```

Prepend ship to spur of purl

    ~zod/main=> (need (epur 'http://123.1.1.1/me.ham'))
    [p=[p=%.n q=~ r=[%.n p=.123.1.1.1]] q=[p=[~ ~.ham] q=<|me|>] r=~]
    ~zod/main=> (earl ~zod (need (epur 'http://123.1.1.1/me.ham')))
    [p=[p=%.n q=~ r=[%.n p=.123.1.1.1]] q=[p=[~ ~.ham] q=<|zod me|>] r=~]
    ~zod/main=> (earl ~pittyp (need (epur 'http://123.1.1.1/me.ham')))
    [p=[p=%.n q=~ r=[%.n p=.123.1.1.1]] q=[p=[~ ~.ham] q=<|pittyp me|>] r=~]
    ~zod/main=> (earn (earl ~pittyp (need (epur 'http://123.1.1.1/me.ham'))))
    "http://123.1.1.1/pittyp/me"

###++earn

```
++  earn                                                ::  purl to tape
  |^  |=  pul=purl
      ^-  tape
      :(weld (head p.pul) "/" (body q.pul) (tail r.pul))
  ::
```

Render purl to tape


    ~zod/main=> (earn [| ~ [%| .127.0.0.1]] [~ ~] ~)
    "http://127.0.0.1/"
    ~zod/main=> (earn [| ~ `/com/google/www] [~ ~] ~)
    "http://www.google.com/"
    ~zod/main=> (earn [& ~ `/com/google/www] [~ ~] ~)
    "https://www.google.com/"
    ~zod/main=> (earn [& `200 `/com/google/www] [~ ~] ~)
    "https://www.google.com:200/"
    ~zod/main=> (earn [& `200 `/com/google/www] [~ /search] ~)
    "https://www.google.com:200/search"
    ~zod/main=> (earn [& ~ `/com/google/www] [`%html /search] ~)
    "https://www.google.com/search"
    ~zod/main=> (earn [& ~ `/com/google/www] [~ /search] [%q 'urbit'] ~)
    "https://www.google.com/search?q=urbit"
    ~zod/main=> (earn [& ~ `/com/google/www] [~ /search] [%q 'urbit escaping?'] ~)
    "https://www.google.com/search?q=urbit%20escaping%3F"

###++body
  
```
  ++  body
    |=  pok=pork  ^-  tape
    ?~  q.pok  ~
    |-
    =+  seg=(trip i.q.pok)
    ?~  t.q.pok
      ?~(p.pok seg (welp seg '.' (trip u.p.pok)))
    (welp seg '/' $(q.pok t.q.pok))
  ::
  
```

Render URL path

    ~zod/main=> (body:earn ~ /foo/mol/lok)
    "foo/mol/lok"
    ~zod/main=> (body:earn `%htm /foo/mol/lok)
    "foo/mol/lok.htm"
    ~zod/main=> (body:earn `%htm /)
    ""

###++head
  
```
  ++  head
    |=  har=hart
    ^-  tape
    ;:  weld
      ?:(&(p.har !=([& /localhost] r.har)) "https://" "http://")
    ::
      ?-  -.r.har
        |  (trip (rsh 3 1 (scot %if p.r.har)))
        &  =+  rit=(flop p.r.har)
           |-  ^-  tape
           ?~(rit ~ (weld (trip i.rit) ?~(t.rit "" `tape`['.' $(rit t.rit)])))
      ==
    ::
      ?~(q.har ~ `tape`[':' (trip (rsh 3 2 (scot %ui u.q.har)))])
    ==
  ::
```

Render URL beginning

    ~zod/main=> (head:earn | ~ %| .127.0.0.1)
    "http://127.0.0.1"
    ~zod/main=> (head:earn & ~ %| .127.0.0.1)
    "https://127.0.0.1"
    ~zod/main=> (head:earn & [~ 8.080] %| .127.0.0.1)
    "https://127.0.0.1:8080"
    ~zod/main=> (head:earn & [~ 8.080] %& /com/google/www)
    "https://www.google.com:8080"

###++tail
  
```
  ++  tail
    |=  kay=quay
    ^-  tape
    ?:  =(~ kay)  ~
    :-  '?'
    |-  ^-  tape
    ?~  kay  ~
    ;:  weld
      (urle (trip p.i.kay))
      "="
      (urle (trip q.i.kay))
      ?~(t.kay ~ `tape`['&' $(kay t.kay)])
    ==
  --
::
```

Render query string

    ~zod/main=> (tail:earn ~)
    ""
    ~zod/main=> (tail:earn [%ask 'bid'] ~)
    "?ask=bid"
    ~zod/main=> (tail:earn [%ask 'bid'] [%make 'well'] ~)
    "?ask=bid&make=well"


###++epur

```
++  epur                                                ::  url/header parser
  =<  |=(a=cord (rush a apex))
  |%
```

Toplevel url parser

    ~zod/main=> (epur 'http://127.0.0.1/')
    [~ [p=[p=%.n q=~ r=[%.n p=.127.0.0.1]] q=[p=~ q=<||>] r=~]]
    ~zod/main=> (epur 'http://www.google.com/')
    [~ [p=[p=%.n q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<||>] r=~]]
    ~zod/main=> (epur 'https://www.google.com/')
    [~ [p=[p=%.y q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<||>] r=~]]
    ~zod/main=> (epur 'https//www.google.com/')
    ~
    ~zod/main=> (epur 'https://www.google.com:200/')
    [~ [p=[p=%.y q=[~ 200] r=[%.y p=<|com google www|>]] q=[p=~ q=<||>] r=~]]
    ~zod/main=> (epur 'https://www.google.com:200/search')
    [ ~
      [p=[p=%.y q=[~ 200] r=[%.y p=<|com google www|>]] q=[p=~ q=<|search|>] r=~]
    ]
    ~zod/main=> (epur 'https://www.google.com/search')
    [~ [p=[p=%.y q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<|search|>] r=~]]
    ~zod/main=> (epur 'https://www.google.com/search?q=urbit')
    [ ~ 
      [ p=[p=%.y q=~ r=[%.y p=<|com google www|>]]
        q=[p=~ q=<|search|>]
        r=~[[p='q' q='urbit']]
      ]
    ]
    ~zod/main=> (epur 'https://www.google.com/search?q=urb it')
    ~
    ~zod/main=> (epur 'https://www.google.com/search?q=urb%20it')
    [ ~
      [ p=[p=%.y q=~ r=[%.y p=<|com google www|>]] 
        q=[p=~ q=<|search|>] 
        r=~[[p='q' q='urb it']]
      ]
    ]
    ~zod/main=> (epur 'https://www.google.com/search?q=urbit%20escaping%3F')
    [ ~ 
      [ p=[p=%.y q=~ r=[%.y p=<|com google www|>]] 
        q=[p=~ q=<|search|>]
        r=~[[p='q' q='urbit escaping?']]
      ]
    ]


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

URL parsing rule

    ~zod/main=> (auri:epur [1 1] "http://127.0.0.1/")
    [ p=[p=1 q=18] 
        q
      [ ~
          u
        [ p=[p=[p=%.n q=~ r=[%.n p=.127.0.0.1]] q=[p=~ q=<||>] r=~]
          q=[p=[p=1 q=18] q=""]
        ]
      ]
    ]
    ~zod/main=> (auri:epur [1 1] "http://www.google.com/")
    [ p=[p=1 q=23]
        q
      [ ~
         u
        [ p=[p=[p=%.n q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<||>] r=~] 
          q=[p=[p=1 q=23] q=""]
        ]
      ]
    ]
    ~zod/main=> (auri:epur [1 1] "https://www.google.com/")
    [ p=[p=1 q=24]
        q
      [ ~
         u
        [ p=[p=[p=%.y q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<||>] r=~] 
          q=[p=[p=1 q=24] q=""]
        ]
      ]
    ]
    ~zod/main=> (auri:epur [1 1] "https//www.google.com/")
    [ p=[p=1 q=6] q=~]
    ~zod/main=> (auri:epur [1 1] "https://www.google.com:200/")
    [ p=[p=1 q=28]
      q=[~ u=[p=[p=[p=%.y q=[~ 200] r=[%.y p=<|com google www|>]] q=[p=~ q=<||>] r=~] q=[p=[p=1 q=28] q=""]]]
    ]
    ~zod/main=> (auri:epur [1 1] "https://www.google.com:200/search")
    [ p=[p=1 q=34]
      q=[~ u=[p=[p=[p=%.y q=[~ 200] r=[%.y p=<|com google www|>]] q=[p=~ q=<|search|>] r=~] q=[p=[p=1 q=34] q=""]]]
    ]
    ~zod/main=> (auri:epur [1 1] "https://www.google.com/search")
    [ p=[p=1 q=30]
      q=[~ u=[p=[p=[p=%.y q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<|search|>] r=~] q=[p=[p=1 q=30] q=""]]]
    ]
    ~zod/main=> (auri:epur [1 1] "https://www.google.com/search?q=urbit")
    [ p=[p=1 q=38]
        q
      [ ~
          u
        [ p=[p=[p=%.y q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<|search|>] r=~[[p='q' q='urbit']]]
          q=[p=[p=1 q=38] q=""]
        ]
      ]
    ]
    ~zod/main=> (auri:epur [1 1] "https://www.google.com/search?q=urb it")
    [ p=[p=1 q=36]
        q
      [ ~
          u
        [ p=[p=[p=%.y q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<|search|>] r=~[[p='q' q='urb']]]
          q=[p=[p=1 q=36] q=" it"]
        ]
      ]
    ]
    ~zod/main=> (auri:epur [1 1] "https://www.google.com/search?q=urb%20it")
    [ p=[p=1 q=41]
        q
      [ ~
          u
        [ p=[p=[p=%.y q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<|search|>] r=~[[p='q' q='urb it']]]
          q=[p=[p=1 q=41] q=""]
        ]
      ]
    ]
    ~zod/main=> (auri:epur [1 1] "https://www.google.com/search?q=urbit%20escaping%3F")
    [ p=[p=1 q=52]
        q
      [ ~
          u
        [ p=[p=[p=%.y q=~ r=[%.y p=<|com google www|>]] q=[p=~ q=<|search|>] r=~[[p='q' q='urbit escaping?']]]
          q=[p=[p=1 q=52] q=""]
        ]
      ]
    ]


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
