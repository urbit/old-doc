##section 2eD

###++bend

```
++  bend                                                ::  conditional comp
  ~/  %bend
  |*  raq=_|*([a=* b=*] [~ u=[a b]])
  ~/  %fun
  |*  [vex=edge sab=_rule]
  ?~  q.vex
    vex
  =+  yit=(sab q.u.q.vex)
  =+  yur=(last p.vex p.yit)
  ?~  q.yit
    [p=yur q=q.vex]
  =+  vux=(raq p.u.q.vex p.u.q.yit)
  ?~  vux
    [p=yur q=q.vex]
  [p=yur q=[~ u=[p=u.vux q=q.u.q.yit]]]
::
```

Parsing composer: treat each following rule as an optional suffix, using a gate to 
compose its result or reject it.

    ~zod/try=> (scan "a" ;~((bend |=([a=char b=char] ?.(=(a b) ~ (some +(a))))) prn prn))
    ~~a
    ~zod/try=> (scan "aa" ;~((bend |=([a=char b=char] ?.(=(a b) ~ (some +(a))))) prn prn))
    ~~b
    ~zod/try=> (scan "ba" ;~((bend |=([a=char b=char] ?.(=(a b) ~ (some +(a))))) prn prn))
    ! {1 3}
    ! exit

###++comp

```
++  comp
  ~/  %comp
  |*  raq=_|*([a=* b=*] [a b])                          ::  arbitrary compose
  ~/  %fun
  |*  [vex=edge sab=_rule]
  ?~  q.vex
    vex
  =+  yit=(sab q.u.q.vex)
  =+  yur=(last p.vex p.yit)
  ?~  q.yit
    [p=yur q=q.yit]
  [p=yur q=[~ u=[p=(raq p.u.q.vex p.u.q.yit) q=q.u.q.yit]]]
::
```

Parsing composer: use a gate to consolidate the results of several rules.

    ~zod/try=> (scan "123" ;~((comp |=([a=@u b=@u] (add a b))) dit dit dit))
    6
    ~zod/try=> (scan "12" ;~((comp |=([a=@u b=@u] (add a b))) dit dit dit))
    ! {1 3}
    ! exit


###++glue

```
++  glue                                                ::  add rule
  ~/  %glue
  |*  bus=_rule
  ~/  %fun
  |*  [vex=edge sab=_rule]
  (plug vex ;~(pfix bus sab))
::
```

Parsing composer: parse delimited tuple

    ~zod/try=> (scan "200|mal|bon" ;~((glue bar) dem sym sym))
    [q=200 7.102.829 7.237.474]
    ~zod/try=> `[@u @tas @tas]`(scan "200|mal|bon" ;~((glue bar) dem sym sym))
    [200 %mal %bon]

###++less

```
++  less                                                ::  no first and second
  |*  [vex=edge sab=_rule]
  ?~  q.vex
    =+  roq=(sab)
    [p=(last p.vex p.roq) q=q.roq]
  vex(q ~)
::
```

Parsing composer: negative lookahead.

    ~zod/try=> (scan "sas-/lo" (star ;~(less lus bar prn)))
    "sas-/lo"
    ~zod/try=> (scan "sas-/l+o" (star ;~(less lus bar prn)))
    ! {1 8}
    ! exit
    ~zod/try=> (scan "sas|-/lo" (star ;~(less lus bar prn)))
    ! {1 5}
    ! exit

###++pfix

```
++  pfix                                                ::  discard first rule
  ~/  %pfix
  (comp |*([a=* b=*] b))
::
```

Parsing composer: ignore prefix

    ~zod/try=> `@t`(scan "%him" ;~(pfix cen sym))
    'him'
    ~zod/try=> (scan "+++10" ;~(pfix (star lus) dem))
    q=10

###++plug

```
++  plug                                                ::  first then second
  ~/  %plug
  |*  [vex=edge sab=_rule]
  ?~  q.vex
    vex
  =+  yit=(sab q.u.q.vex)
  =+  yur=(last p.vex p.yit)
  ?~  q.yit
    [p=yur q=q.yit]
  [p=yur q=[~ u=[p=[p.u.q.vex p.u.q.yit] q=q.u.q.yit]]]
::
```

Parsing composer: match using sequence of rules.

    ~zod/try=> (scan "1..20" ;~(plug dem dot dot dem))
    [q=1 ~~~. ~~~. q=20]
    ~zod/try=> (scan "moke/~2014.1.1" ;~(plug sym fas nuck:so))
    [1.701.539.693 ~~~2f. [% p=[p=~.da q=170.141.184.500.766.106.671.844.917.172.921.958.400]]]
    ~zod/try=> ;;(,[@tas @t ~ %da @da] (scan "moke/~2014.1.1" ;~(plug sym fas nuck:so)))
    [%moke '/' ~ %da ~2014.1.1]

###++pose

```
++  pose                                                ::  first or second
  ~/  %pose
  |*  [vex=edge sab=_rule]
  ?~  q.vex
    =+  roq=(sab)
    [p=(last p.vex p.roq) q=q.roq]
  vex
```

Parsing composer: match either rule.

    ~zod/try=> `@t`(scan "+" ;~(pose lus tar cen))
    '+'
    ~zod/try=> `@t`(scan "*" ;~(pose lus tar cen))
    '*'
    ~zod/try=> `@t`(scan "%" ;~(pose lus tar cen))
    '%'
    ~zod/try=> `@t`(scan "-" ;~(pose lus tar cen))
    ! {1 1}
    ! exit


###++simu

```
++  simu                                                ::  first and second
  |*  [vex=edge sab=_rule]
  ?~  q.vex
    vex
  =+  roq=(sab)
  roq
::
```

Parsing composer: verify that first rule matches, then parse with second.

    ~zod/try=> (scan "~zod" scat:vast)
    [%dtzy p=%p q=0]
    ~zod/try=> (scan "%zod" scat:vast)
    [%dtzz p=%tas q=6.582.138]
    ~zod/try=> (scan "%zod" ;~(simu cen scat:vast))
    [%dtzz p=%tas q=6.582.138]
    ~zod/try=> (scan "~zod" ;~(simu cen scat:vast))
    ! {1 1}
    ! exit

###++sfix

```
++  sfix                                                ::  discard second rule
  ~/  %sfix
  (comp |*([a=* b=*] a))
```

Parsing composer: ignore suffix

    ~zod/try=> `@t`(scan "him%" ;~(sfix sym cen))
    'him'
    ~zod/try=> (scan "10+++" ;~(sfix dem (star lus)))
    q=10
