##section 3bC, UTC                      ::  Gregorianonly

###++dawn

```
++  dawn                                                ::  Jan 1 weekday
  |=  yer=@ud
  =+  yet=(sub yer 1)
  %-  mod  :_  7
  :(add 1 (mul 5 (mod yet 4)) (mul 4 (mod yet 100)) (mul 6 (mod yet 400)))
::
```

XX document

###++daws

```
++  daws                                                ::  date weekday
  |=  yed=date
  %-  mod  :_  7
  (add (dawn y.yed) (sub (yawn [y.yed m.yed d.t.yed]) (yawn y.yed 1 1)))
::
```

XX document

###++deal

```
++  deal                                                ::  to leap sec time
  |=  yer=@da
  =+  n=0
  =+  yud=(yore yer)
  |-  ^-  date
  ?:  (gte yer (add (snag n lef:yu) ~s1))
    (yore (year yud(s.t (add n s.t.yud))))
  ?:  &((gte yer (snag n lef:yu)) (lth yer (add (snag n lef:yu) ~s1)))
    yud(s.t (add +(n) s.t.yud))
  ?:  =(+(n) (lent lef:yu))
    (yore (year yud(s.t (add +(n) s.t.yud))))
  $(n +(n))
::
```

XX document

###++lead

```
++  lead                                                ::  from leap sec time
  |=  ley=date
  =+  ler=(year ley)
  =+  n=0
  |-  ^-  @da
  =+  led=(sub ler (mul n ~s1))
  ?:  (gte ler (add (snag n les:yu) ~s1))
    led
  ?:  &((gte ler (snag n les:yu)) (lth ler (add (snag n les:yu) ~s1)))
    ?:  =(s.t.ley 60)
      (sub led ~s1)
    led
  ?:  =(+(n) (lent les:yu))
    (sub led ~s1)
  $(n +(n))
::
```

XX document

###++dust

```
++  dust                                                ::  print UTC format
  |=  yed=date
  ^-  tape
  =+  wey=(daws yed)
  ;:  weld
      `tape`(snag wey (turn wik:yu |=(a=tape (scag 3 a))))
      ", "  ~(rud at d.t.yed)  " "
      `tape`(snag (dec m.yed) (turn mon:yu |=(a=tape (scag 3 a))))
      " "  (scag 1 ~(rud at y.yed))  (slag 2 ~(rud at y.yed))  " "
      ~(rud at h.t.yed)  ":"  ~(rud at m.t.yed)  ":"  ~(rud at s.t.yed)
      " "  "+0000"
  ==
::
```

XX document

###++stud

```
++  stud                                                ::  parse UTC format
  |=  cud=tape
  ^-  (unit date)
  =-  ?~  tud  ~ 
      `[[%.y &3.u.tud] &2.u.tud &1.u.tud &4.u.tud &5.u.tud &6.u.tud ~]
  ^=  tud
  %+  rust  cud
  ;~  plug
    ;~(pfix (stun [5 5] next) dim:ag)
  ::
    %+  cook
      |=  a=tape
      =+  b=0
      |-  ^-  @
      ?:  =(a (snag b (turn mon:yu |=(a=tape (scag 3 a)))))
          +(b)
      $(b +(b))
    (ifix [ace ace] (star alf))
  ::
    ;~(sfix dim:ag ace)  
    ;~(sfix dim:ag col)
    ;~(sfix dim:ag col)  
    dim:ag  
    (cold ~ (star next))
  ==
::
```

XX document

###++unt

```
++  unt                                                 ::  UGT to UTC time
  |=  a=@
  (div (sub a ~1970.1.1) (bex 64))
::
```

XX document

###++yu

```
++  yu                                                  ::  UTC format constants
  |%
```

XX document

###++mon

```
  ++  mon  ^-  (list tape)
    :~  "January"  "February"  "March"  "April"  "May"  "June"  "July"
        "August"  "September"  "October"  "November"  "December"
    ==
  ::
```

XX document

###++wik

```
  ++  wik  ^-  (list tape)
    :~  "Sunday"  "Monday"  "Tuesday"  "Wednesday"  "Thursday"
        "Friday"  "Saturday"
    ==
  ::
```

XX document

###++les

```
  ++  les  ^-  (list ,@da)
    :~  ~2012.7.1  ~2009.1.1  ~2006.1.1  ~1999.1.1  ~1997.7.1  ~1996.1.1
        ~1994.7.1  ~1993.7.1  ~1992.7.1  ~1991.1.1  ~1990.1.1  ~1988.1.1
        ~1985.7.1  ~1983.7.1  ~1982.7.1  ~1981.7.1  ~1980.1.1  ~1979.1.1
        ~1978.1.1  ~1977.1.1  ~1976.1.1  ~1975.1.1  ~1974.1.1  ~1973.1.1
        ~1972.7.1
    ==
```

XX document

###++lef

```
  ++  lef  ^-  (list ,@da)
    :~  ~2012.6.30..23.59.59   ~2008.12.31..23.59.58
        ~2005.12.31..23.59.57  ~1998.12.31..23.59.56
        ~1997.6.30..23.59.55   ~1995.12.31..23.59.54
        ~1994.6.30..23.59.53   ~1993.6.30..23.59.52
        ~1992.6.30..23.59.51   ~1990.12.31..23.59.50
        ~1989.12.31..23.59.49  ~1987.12.31..23.59.48
        ~1985.6.30..23.59.47   ~1983.6.30..23.59.46
        ~1982.6.30..23.59.45   ~1981.6.30..23.59.44
        ~1979.12.31..23.59.43  ~1978.12.31..23.59.42
        ~1977.12.31..23.59.41  ~1976.12.31..23.59.40
        ~1975.12.31..23.59.39  ~1974.12.31..23.59.38
        ~1973.12.31..23.59.37  ~1972.12.31..23.59.36
        ~1972.6.30..23.59.35
    ==
::
```

XX document

