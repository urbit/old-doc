##section 2eL, formatting (path)

###++ab

```
++  ab
  |%
```

A core containing numeric parser primitives.

    /~zod/try=> ab
    <36.ecc 414.gly 100.xkc 1.ypj %164>

###++bix

Parse hex digit pair

```
  ++  bix  (bass 16 (stun [2 2] six))
```

Parsing rule. Parses a pair of base-16 digits. Used in escapes.

    /~zod/try=> (scan "07" bix:ab)
    q=7
    /~zod/try=> (scan "51" bix:ab)
    q=81
    /~zod/try=> (scan "a3" bix:ab)
    q=163

###++hif

Parse phonemic pair

```
  ++  hif  (boss 256 ;~(plug tip tiq (easy ~)))
```

Parsing rule. Parses an atom of odor [@pE](), a phrase of two bytes encoded phonetically.

    /~zod/try=> (scan "doznec" hif:ab)
    q=256
    /~zod/try=> (scan "pittyp" hif:ab)
    q=48.626

###++huf

Parse two phonemic pairs

```
  ++  huf  %+  cook
               |=([a=@ b=@] (wred:un ~(zug mu ~(zag mu [a b]))))
             ;~(plug hif ;~(pfix hep hif))
```

Parsing rule. Parses and unscrambles and atom of odor [@pF](), a phrase of two two-byte pairs that are encoded (and scrambled) phonetically.

    /~zod/try=> (scan "pittyp-pittyp" huf:ab)
    328.203.557
    /~zod/try=> (scan "tasfyn-partyv" huf:ab)
    65.792
    /~zod/try=> `@ux`(scan "tasfyn-partyv" huf:ab)
    0x1.0100

###++hyf

Parse 8 phonemic bytes

```
  ++  hyf  (bass 0x1.0000.0000 ;~(plug huf ;~(pfix hep huf) (easy ~)))
```

Parsing rule. Parses an atom of odor [@pG](), a phrase of eight of phonemic bytes. 

    /~zod/try=> (scan "sondel-forsut-tillyn-nillyt" hyf:ab)
    q=365.637.097.828.335.095
    /~zod/try=> `@u`~sondel-forsut-tillyn-nillyt
    365.637.097.828.335.095

###++pev

Parse up to 4 base-32

```
  ++  pev  (bass 32 ;~(plug sev (stun [0 4] siv)))
```

Parsing rule. Parses up to four base-32 digits

    /~zod/try=> (scan "a" pev:ab)
    q=10
    /~zod/try=> (scan "290j" pev:ab)
    q=74.771
    /~zod/try=> `@`0v290j
    74.771

###++pew

Parse up to 4 base-64

```
  ++  pew  (bass 64 ;~(plug sew (stun [0 4] siw)))
```

Parsing rule. Parses up to four base-64 digits.

    /~zod/try=> (scan "Q" pew:ab)
    q=52
    /~zod/try=> (scan "aQ~9" pew:ab)
    q=2.838.473
    /~zod/try=> `@`0waQ~9
    2.838.473

###++piv

Parse 5 base-32

```
  ++  piv  (bass 32 (stun [5 5] siv))
```

Parsing rule. Parses exactly five base-32 digits.

    /~zod/try=> (scan "10b3l" piv:ab)
    q=1.059.957
    ~zod/try=> (scan "1" piv:ab)
        ! {1 2}
        ! exit

###++piw

Parse 5 base-64

```
  ++  piw  (bass 64 (stun [5 5] siw))
```

Parsing rule. Parses exactly five base-64 digits.

    /~zod/try=> (scan "2C-pZ" piw:ab)
    q=43.771.517
    ~zod/socialnet=> (scan "2" piv:ab)
    ! {1 2}
    ! exit

###++qeb

Parse up to 4 digit binary

```
  ++  qeb  (bass 2 ;~(plug seb (stun [0 3] sib)))
```

Parsing rule. Parses a binary number of up to 4 digits in length.

    /~zod/try=> (scan "1" qeb:ab)
    q=1
    /~zod/try=> (scan "101" qeb:ab)
    q=5

###++qex

Parse up to 4 digit hex

```
  ++  qex  (bass 16 ;~(plug sex (stun [0 3] hit)))
```

Parsing rule. Parses a hexadecimal number of up to 4 digits in length.

    /~zod/try=> (scan "c" qex:ab)
    q=12
    /~zod/try=> (scan "ca" qex:ab)
    q=202
    /~zod/try=> (scan "18ac" qex:ab)
    q=6.316

###++qib

Parse 4 bin digits

```
  ++  qib  (bass 2 (stun [4 4] sib))
```

Parsing rule. Parses four binary digits.

    /~zod/try=> (scan "0001" qib:ab)
    q=1
    /~zod/try=> (scan "0100" qib:ab)
    q=4


###++qix

Parse 4 hexadecimal 

```
  ++  qix  (bass 16 (stun [4 4] six))
```

Parsing rule. Parses exactly four hexadecimal digits.

    /~zod/try=> (scan "0100" qix:ab)
    q=256
    /~zod/try=> (scan "10ff" qix:ab)
    q=4.351
    ~zod/socialnet=> (scan "0" qix:ab)
    ! {1 2}
    ! exit

###++seb

Parse 1

```
  ++  seb  (cold 1 (just '1'))
```

Parsing rule. Parses the number 1.

    /~zod/try=> (scan "1" seb:ab)
    1
    /~zod/try=> (scan "0" seb:ab)
    ! /~zod/try/~2014.10.23..22.34.21..bfdd/:<[1 1].[1 18]>
    ! {1 1}
    /~zod/try=> (scan "2" seb:ab)
    ! /~zod/try/~2014.10.23..22.34.29..d399/:<[1 1].[1 18]>
    ! {1 1}

###++sed

Parse decimal

```
  ++  sed  (cook |=(a=@ (sub a '0')) (shim '1' '9'))
```

Parsing rule. Parses a nonzero decimal digit.

    /~zod/try=> (scan "5" sed:ab)
    5
    ~zod/socialnet=> (scan "55" sed:ab)
    ! {1 2}
    ! exit

###++sev

Parse base-32

```
  ++  sev  ;~(pose sed sov)
```

Parsing rule. Parses a nonzero base-32 digit

    /~zod/try=> (scan "c" sev:ab)
    12

###++sew

Parse base-64

```
  ++  sew  ;~(pose sed sow)
```

Parsing rule. Parses nonzero base-64 digit

    /~zod/try=> (scan "M" sew:ab)
    48

###++sex

Parse hexadecimal

```
  ++  sex  ;~(pose sed sox)
```

Parsing rule. Parses a nonzero hexadecimal digit.

    /~zod/try=> (scan "e" sex:ab)
    14

###++sib

Parse binary

```
  ++  sib  (cook |=(a=@ (sub a '0')) (shim '0' '1'))
```

Parsing rule. Parses a binary digit.

    /~zod/try=> (scan "1" sib:ab)
    1

###++siq

```
  ++  siq  ;~  pose
             (shim 'a' 'z')
             (shim 'A' 'Z')
             (shim '0' '9')
             hep
             (cold 32 dot)
             ;~(pfix sig ;~(pose sig dot bix))
           ==
```

Single formal cord character

    /~zod/try=> ~~20.a
    '20 a'
    /~zod/try=> (tape (scan "20.a" (star siq:ab)))
    "20 a"
    /~zod/try=> (tape (scan "20.~43-2" (star siq:ab)))
    "20 C-2"


###++sid

Parse decimal

```
  ++  sid  (cook |=(a=@ (sub a '0')) (shim '0' '9'))
```

Parse decimal digit

    /~zod/try=> (scan "5" sid:ab)
    5

###++siv

Parse base-32

```
  ++  siv  ;~(pose sid sov)
```

Parsing rule. Parses a base-32 digit.

    /~zod/try=> (scan "c" siv:ab)
    12

###++siw

Parse base-64

```
  ++  siw  ;~(pose sid sow)
```

Parsing rule. Parses a base64 digit.

    /~zod/try=> (scan "M" siw:ab)
    48

###++six

Parse hexadecimal

```
  ++  six  ;~(pose sid sox)
```

Parse hexadecimal digit

    /~zod/try=> (scan "e" six:ab)
    14

###++sov

Parse base-32

```
  ++  sov  (cook |=(a=@ (sub a 87)) (shim 'a' 'v'))
```

Parsing rule. Parses base-32 letter.

    /~zod/try=> (scan "c" sov:ab)
    12

###++sow

Parse base-64

```
  ++  sow  ;~  pose
             (cook |=(a=@ (sub a 87)) (shim 'a' 'z'))
             (cook |=(a=@ (sub a 29)) (shim 'A' 'Z'))
             (cold 62 (just '-'))
             (cold 63 (just '~'))
           ==
```

Parsing rule. Parses a base-64 letter/symbol.

    /~zod/try=> (scan "M" sow:ab)
    48

###++sox

Parse hex letter

```
  ++  sox  (cook |=(a=@ (sub a 87)) (shim 'a' 'f'))
```

Parse hexadecimal letter

    /~zod/try=> (scan "e" sox:ab)
    14

###++ted

Parse 3 decimal digits

```
  ++  ted  (bass 10 ;~(plug sed (stun [0 2] sid)))
```

Parse decimal number of up to 3 digits

    /~zod/try=> (scan "21" ted:ab)
    q=21
    /~zod/try=> (scan "214" ted:ab)
    q=214
    /~zod/try=> (scan "2140" ted:ab)
    {1 4}


###++tip

Leading phonetic byte

```
  ++  tip  (sear |=(a=@ (ins:po a)) til)
```

Parsing rule. Parses the leading phonetic byte that represents a syllable.

    /~zod/try=> (scan "doz" tip:ab)
    0
    /~zod/try=> (scan "pit" tip:ab)
    242

###++tiq

Trailing phonetic syllable

```
  ++  tiq  (sear |=(a=@ (ind:po a)) til)
```

Parsing rule. Parses the trailing phonetic byte that represents a syllable.

    /~zod/try=> (scan "zod" tiq:ab)
    0
    /~zod/try=> (scan "nec" tiq:ab)
    1

###++tid

Parse 3 decimal digits

```
  ++  tid  (bass 10 (stun [3 3] sid))
```

Parsing rule. Parses exactly three decimal digits.
    
    /~zod/try=> (scan "013" tid:ab)
    q=13
    ~zod/socialnet=> (scan "01" tid:ab)
    ! {1 3}
    ! exit

###++til

Parse 3 lowercase

```
  ++  til  (boss 256 (stun [3 3] low))
```

Parsing rule. Parses exactly three lowercase letters.

    /~zod/try=> (scan "mer" til:ab)
    q=7.497.069
    /~zod/try=> `@t`(scan "mer" til:ab)
    'mer'
    ~zod/socialnet=> (scan "me" til:ab)
    ! {1 3}
    ! exit

###++urs

Parse span characters

```
  ++  urs  %+  cook
             |=(a=tape (rap 3 ^-((list ,@) a)))
           (star ;~(pose nud low hep dot sig cab))
```

Parsing rule. Parses characters

    ~zod/socialnet=> `@ta`(scan "asa-lom_tak" urs:ab)
    ~.asa-lom_tak 
    ~zod/try=> `@t`(scan "asa-lom_tak" urs:ab)
    'asa-lom_tak'

###++urt

Parse non-'_' span

```
  ++  urt  %+  cook
             |=(a=tape (rap 3 ^-((list ,@) a)))
           (star ;~(pose nud low hep dot sig))
```

Parsing rule. Parses non-'_' span characters.

    /~zod/try=> `@t`(scan "asa-lom.t0k" urt:ab)
    'asa-lom.t0k'

###++voy

Parse bas, soq, or bix

```
  ++  voy  ;~(pfix bas ;~(pose bas soq bix))
```

Parsing rule. Parses an escaped backslash, single quote, or hex pair byte.

    /~zod/try=> (scan "\\0a" voy:ab)
    q=10
    /~zod/try=> (scan "\\'" voy:ab)
    q=39

###++ag

Top-level atom parsers

```
++  ag
  |%
```

Core containing toplevel atom parsers.

    /~zod/try=> ag
    <14.vpu 414.mof 100.xkc 1.ypj %164>

###++ape

```
  ++  ape  |*(fel=_rule ;~(pose (cold 0 (just '0')) fel))
```

Parse 0 or rule

    /~zod/try=> (scan "202" (star (ape:ag (just '2'))))
    ~[~~2 ~~ ~~2]

###++bay

```
  ++  bay  (ape (bass 16 ;~(plug qeb:ab (star ;~(pfix dog qib:ab)))))
```

Parse binary number.

    /~zod/try=> (scan "10.0110" bay:ag)
    q=38

###++bip

```
  ++  bip  =+  tod=(ape qex:ab)
           (bass 0x1.0000 ;~(plug tod (stun [7 7] ;~(pfix dog tod))))
```

IPv6 address

    /~zod/try=> (scan "0.0.ea.3e6c.0.0.0.0" bip:ag)
    q=283.183.420.760.121.105.516.068.864
    /~zod/try=> `@is`(scan "0.0.ea.3e6c.0.0.0.0" bip:ag)
    .0.0.ea.3e6c.0.0.0.0

###++dem

```
  ++  dem  (ape (bass 1.000 ;~(plug ted:ab (star ;~(pfix dog tid:ab)))))
```

Decimal number, with dots

    /~zod/try=> (scan "52" dem:ag)
    q=52
    /~zod/try=> (scan "13.507" dem:ag)
    q=13.507

###++dim

```
  ++  dim  (ape (bass 10 ;~(plug sed:ab (star sid:ab))))
```

Decimal number

    /~zod/try=> (scan "52" dim:ag)
    q=52
    /~zod/try=> (scan "13507" dim:ag)
    q=13.507

###++dum

```
  ++  dum  (bass 10 (plus sid:ab))
```

Decmial number with leading zeroes

    /~zod/try=> (scan "52" dum:ag)
    q=52
    /~zod/try=> (scan "0000052" dum:ag)
    q=52
    /~zod/try=> (scan "13507" dim:ag)
    q=13.507

###++fed

```
  ++  fed  ;~  pose
             (bass 0x1.0000.0000.0000.0000 (most doh hyf:ab))
             huf:ab
             hif:ab
             tiq:ab
           ==
```

Phonetic base

    /~zod/try=> (scan "zod" fed:ag)
    0
    /~zod/try=> (scan "nec" fed:ag)
    1
    /~zod/try=> (scan "sondel" fed:ag)
    9.636
    /~zod/try=> ~tillyn-nillyt
    ~tillyn-nillyt
    /~zod/try=> (scan "tillyn-nillyt" fed:ag)
    3.569.565.175
    /~zod/try=> (scan "tillyn-nillyt-tasfyn-partyv" fed:ag)
    15.331.165.687.565.582.592
    /~zod/try=> (scan "tillyn-nillyt-tasfyn-partyv--novweb-talrud-talmud-sonfyr" fed:ag)
    282.810.089.790.159.633.869.501.053.313.363.681.181


###++hex

```
  ++  hex  (ape (bass 0x1.0000 ;~(plug qex:ab (star ;~(pfix dog qix:ab)))))
```

Hexadecimal number

    /~zod/try=> (scan "4" hex:ag)
    q=4
    /~zod/try=> (scan "1a" hex:ag)
    q=26
    /~zod/try=> (scan "3.ac8d" hex:ag)
    q=240.781
    /~zod/try=> `@ux`(scan "3.ac8d" hex:ag)
    0x3.ac8d

###++lip

```
  ++  lip  =+  tod=(ape ted:ab)
           (bass 256 ;~(plug tod (stun [3 3] ;~(pfix dog tod))))
```

IPv4 address

    /~zod/try=> (scan "127.0.0.1" lip:ag)
    q=2.130.706.433
    /~zod/try=> `@if`(scan "127.0.0.1" lip:ag)
    .127.0.0.1
    /~zod/try=> `@if`(scan "8.8.8.8" lip:ag)
    .8.8.8.8

###++tyq

```
  ++  tyq  (cook |=(a=(list ,@) (rap 3 a)) (plus siq:ab))
```

Formal cord form

    /~zod/try=> (scan "20.a" tyq:ag)
    1.629.499.442
    /~zod/try=> `@t`(scan "20.a" tyq:ag)
    '20 a'
    /~zod/try=> ~~20.a
    '20 a'
    /~zod/try=> `@t`(scan "20.~43-2" tyq:ag)
    '20 C-2'

###++viz

```
  ++  viz  (ape (bass 0x200.0000 ;~(plug pev:ab (star ;~(pfix dog piv:ab)))))
```

Base32 number, with dots

    /~zod/try=> (scan "e2.ol4pm" viz:ag)
    q=15.125.353.270

###++vum

```
  ++  vum  (bass 32 (plus siv:ab))
```

Raw base32 string

    /~zod/try=> (scan "e2ol4pm" vum:ag)
    q=15.125.353.270

###++wiz

```
  ++  wiz  (ape (bass 0x4000.0000 ;~(plug pew:ab (star ;~(pfix dog piw:ab)))))
  --
::
```

Base64 number 

    /~zod/try=> (scan "e2O.l4Xpm" wiz:ag)
    q=61.764.130.813.526


###++co

```
++  co
  =<  |_  lot=coin
```

Literal rendering engine

    /~zod/try=> ~(. co many/~[`ta/'mo' `ud/5])
    < 3.dhd
      [ [ %many
          [%~ %ta @t]
          [%~ %ud @ud]
          %~
        ]
        <10.utz 3.zid [rex="" <414.hmb 100.xkc 1.ypj %164>]>
      ]
    >


###++rear

```
      ++  rear  |=(rom=tape =>(.(rex rom) rend))
```

Prepend to tape

    ~zod/try=> (~(rear co %$ %ux 200) "--ha")
    "0xc8--ha"
    
###++rent

```
      ++  rent  `@ta`(rap 3 rend)
```

Print to span

    ~zod/try=> ~(rent co %$ %ux 200)
    ~.0xc8
    ~zod/try=> `@t`~(rent co %$ %ux 200)
    '0xc8'


###++rend

```
      ++  rend
        ^-  tape
        ?:  ?=(%blob -.lot)
          ['~' '0' ((v-co 1) (jam p.lot))]
        ?:  ?=(%many -.lot)
          :-  '.'
          |-  ^-  tape
          ?~   p.lot
            ['_' '_' rex]
          ['_' (weld (trip (wack rent(lot i.p.lot))) $(p.lot t.p.lot))]
        =+  [yed=(end 3 1 p.p.lot) hay=(cut 3 [1 1] p.p.lot)]
        |-  ^-  tape
        ?+    yed  (z-co q.p.lot)
            %c   ['~' '-' (weld (rip 3 (wood (tuft q.p.lot))) rex)]
            %d
          ?+    hay  (z-co q.p.lot)
              %a
            =+  yod=(yore q.p.lot)
            =>  ^+(. .(rex ?~(f.t.yod rex ['.' (s-co f.t.yod)])))
            =>  ^+  .
                %=    .
                    rex
                  ?:  &(=(~ f.t.yod) =(0 h.t.yod) =(0 m.t.yod) =(0 s.t.yod))
                    rex
                  =>  .(rex ['.' (y-co s.t.yod)])
                  =>  .(rex ['.' (y-co m.t.yod)])
                  ['.' '.' (y-co h.t.yod)]
                ==
            =>  .(rex ['.' (a-co d.t.yod)])
            =>  .(rex ['.' (a-co m.yod)])
            =>  .(rex ?:(a.yod rex ['-' rex]))
            ['~' (a-co y.yod)]
          ::
              %r
            =+  yug=(yell q.p.lot)
            =>  ^+(. .(rex ?~(f.yug rex ['.' (s-co f.yug)])))
            :-  '~'
            ?:  &(=(0 d.yug) =(0 m.yug) =(0 h.yug) =(0 s.yug))
              ['.' 's' '0' rex]
            =>  ^+(. ?:(=(0 s.yug) . .(rex ['.' 's' (a-co s.yug)])))
            =>  ^+(. ?:(=(0 m.yug) . .(rex ['.' 'm' (a-co m.yug)])))
            =>  ^+(. ?:(=(0 h.yug) . .(rex ['.' 'h' (a-co h.yug)])))
            =>  ^+(. ?:(=(0 d.yug) . .(rex ['.' 'd' (a-co d.yug)])))
            +.rex
          ==
        ::
            %f
          ?:  =(& q.p.lot)
            ['.' 'y' rex]
          ?:(=(| q.p.lot) ['.' 'n' rex] (z-co q.p.lot))
        ::
            %n   ['~' rex]
            %i
          ?+  hay  (z-co q.p.lot)
            %f  ((ro-co [3 10 4] |=(a=@ ~(d ne a))) q.p.lot)
            %s  ((ro-co [4 16 8] |=(a=@ ~(x ne a))) q.p.lot)
          ==
        ::
            %p
          =+  dyx=(met 3 q.p.lot)
          :-  '~'
          ?:  (lte dyx 1)
            (weld (trip (tod:po q.p.lot)) rex)
          ?:  =(2 dyx)
            ;:  weld
              (trip (tos:po (end 3 1 q.p.lot)))
              (trip (tod:po (rsh 3 1 q.p.lot)))
              rex
            ==
          =+  [dyz=(met 5 q.p.lot) fin=|]
          |-  ^-  tape
          ?:  =(0 dyz)
            rex
          %=    $
              fin      &
              dyz      (dec dyz)
              q.p.lot  (rsh 5 1 q.p.lot)
              rex
            =+  syb=(wren:un (end 5 1 q.p.lot))
            =+  cog=~(zig mu [(rsh 4 1 syb) (end 4 1 syb)])
            ;:  weld
              (trip (tos:po (end 3 1 p.cog)))
              (trip (tod:po (rsh 3 1 p.cog)))
              `tape`['-' ~]
              (trip (tos:po (end 3 1 q.cog)))
              (trip (tod:po (rsh 3 1 q.cog)))
              `tape`?:(fin ['-' ?:(=(1 (end 0 1 dyz)) ~ ['-' ~])] ~)
              rex
            ==
          ==
        ::
            %r
          ?+  hay  (z-co q.p.lot)
            %d  
          =+  r=(rlyd q.p.lot)
          ?~  e.r
            ['.' '~' (r-co r)]
          ['.' '~' u.e.r]
            %h  ['.' '~' '~' (r-co (rlyh q.p.lot))]
            %q  ['.' '~' '~' '~' (r-co (rlyq q.p.lot))]
            %s  ['.' (r-co (rlys q.p.lot))]
          ==
        ::
            %u
          =-  (weld p.gam ?:(=(0 q.p.lot) `tape`['0' ~] q.gam))
          ^=  gam  ^-  [p=tape q=tape]
          ?+  hay  [~ ((ox-co [10 3] |=(a=@ ~(d ne a))) q.p.lot)]
            %b  [['0' 'b' ~] ((ox-co [2 4] |=(a=@ ~(d ne a))) q.p.lot)]
            %i  [['0' 'i' ~] ((d-co 1) q.p.lot)]
            %x  [['0' 'x' ~] ((ox-co [16 4] |=(a=@ ~(x ne a))) q.p.lot)]
            %v  [['0' 'v' ~] ((ox-co [32 5] |=(a=@ ~(x ne a))) q.p.lot)]
            %w  [['0' 'w' ~] ((ox-co [64 5] |=(a=@ ~(w ne a))) q.p.lot)]
          ==
        ::
            %s
          %+  weld
            ?:((syn:si q.p.lot) "--" "-")
          $(yed 'u', q.p.lot (abs:si q.p.lot))
        ::
            %t
          ?:  =('a' hay)
            ?:  =('s' (cut 3 [2 1] p.p.lot))
              
              (weld (rip 3 q.p.lot) rex)
            ['~' '.' (weld (rip 3 q.p.lot) rex)]
          ['~' '~' (weld (rip 3 (wood q.p.lot)) rex)]
        ==
      --
  =+  rex=*tape
  =<  |%
      ++  a-co  |=(dat=@ ((d-co 1) dat))
      ++  d-co  |=(min=@ (em-co [10 min] |=([? b=@ c=tape] [~(d ne b) c])))
      ++  r-co
        |=  [syn=? nub=@ der=@ ign=(unit tape) ne=?]
        =>  .(rex ['.' (t-co ((d-co 1) der) ne)])
        =>  .(rex ((d-co 1) nub))
        ?:(syn rex ['-' rex])
      ++  t-co  |=  [a=tape n=?]  ^-  tape 
        ?:  n  a
        ?~  a  ~|(%empty-frac !!)  t.a
      ::
      ++  s-co
        |=  esc=(list ,@)  ^-  tape
        ~|  [%so-co esc]
        ?~  esc
          rex
        :-  '.'
        =>(.(rex $(esc t.esc)) ((x-co 4) i.esc))
        
    ::
      ++  v-co  |=(min=@ (em-co [32 min] |=([? b=@ c=tape] [~(v ne b) c])))
      ++  w-co  |=(min=@ (em-co [64 min] |=([? b=@ c=tape] [~(w ne b) c])))
      ++  x-co  |=(min=@ (em-co [16 min] |=([? b=@ c=tape] [~(x ne b) c])))
      ++  y-co  |=(dat=@ ((d-co 2) dat))
      ++  z-co  |=(dat=@ `tape`['0' 'x' ((x-co 1) dat)])
      --
  ~%  %co  +>  ~
  |%
  ++  em-co
    ~/  %emco
    |=  [[bas=@ min=@] [par=$+([? @ tape] tape)]]
    |=  hol=@
    ^-  tape
    ?:  &(=(0 hol) =(0 min))
      rex
    =+  [rad=(mod hol bas) dar=(div hol bas)]
    %=  $
      min  ?:(=(0 min) 0 (dec min))
      hol  dar
      rex  (par =(0 dar) rad rex)
    ==
  ::
  ++  ox-co
    ~/  %oxco
    |=  [[bas=@ gop=@] dug=$+(@ @)]
    %+  em-co
      [|-(?:(=(0 gop) 1 (mul bas $(gop (dec gop))))) 0]
    |=  [top=? seg=@ res=tape]
    %+  weld
      ?:(top ~ `tape`['.' ~])
    %.  seg
    %+  em-co(rex res)
      [bas ?:(top 0 gop)]
    |=([? b=@ c=tape] [(dug b) c])
  ::
  ++  ro-co
    ~/  %roco
    |=  [[buz=@ bas=@ dop=@] dug=$+(@ @)]
    |=  hol=@
    ^-  tape
    ?:  =(0 dop)
      rex
    =>  .(rex $(dop (dec dop)))
    :-  '.'
    %-  (em-co [bas 1] |=([? b=@ c=tape] [(dug b) c]))
    [(cut buz [(dec dop) 1] hol)]
  --
::
```

Print to tape, using helper arms

    ~zod/try=> ~(rend co ~ %ux 200)
    "0xc8"
    ~zod/try=> ~(rend co %many ~[[%$ ux/200] [%$ p/40]])
    "._0xc8_~~tem__"
    ~zod/try=> ~(rend co ~ %p 32.819)
    "~pillyt"
    ~zod/try=> ~(rend co ~ %ux 18)
    "0x12"
    ~zod/try=> ~(rend co [~ p=[p=%if q=0x7f00.0001]])
    ".127.0.0.1"
    ~zod/try=> `@ux`.127.0.0.1
    2.130.706.433
    ~zod/try=> ~(rend co %many ~[[~ %ud 20] [~ %uw 133] [~ %tas 'sam']])
    "._20_0w25_sam__"
    ~zod/try=> ~(rend co %blob [1 1])
    "~0ph"
    ~zod/try=> ~0ph
    [1 1]
    ~zod/try=> `@uv`(jam [1 1])
    0vph


###++ne

```
++  ne
  |_  tig=@
```

Render digit at base. Helper core.

    ~zod/try=> ~(. ne 20)
    <4.gut [@ud <414.hhh 100.xkc 1.ypj %164>]>


###++d

```
  ++  d  (add tig '0')
```

Decimal

    ~zod/try=> `@t`~(d ne 7)
    '7'

###++x

```
  ++  x  ?:((gte tig 10) (add tig 87) d)
```

Hexadecimal

    ~zod/try=> `@t`~(x ne 7)
    '7'
    ~zod/try=> `@t`~(x ne 14)
    'e'

###++v

```
  ++  v  ?:((gte tig 10) (add tig 87) d)
```

Base 32

    ~zod/try=> `@t`~(v ne 7)
    '7'
    ~zod/try=> `@t`~(v ne 14)
    'e'
    ~zod/try=> `@t`~(v ne 25)
    'p'


###++w

```
  ++  w  ?:(=(tig 63) '~' ?:(=(tig 62) '-' ?:((gte tig 36) (add tig 29) x)))
  --
::
```

Base 64: 0-9a-zA-Z-~

    ~zod/try=> `@t`~(w ne 7)
    '7'
    ~zod/try=> `@t`~(w ne 14)
    'e'
    ~zod/try=> `@t`~(w ne 25)
    'p'
    ~zod/try=> `@t`~(w ne 52)
    'Q'
    ~zod/try=> `@t`~(w ne 61)
    'Z'
    ~zod/try=> `@t`~(w ne 63)
    '~'
    ~zod/try=> `@t`~(w ne 62)
    '-'


###++mu

```
++  mu
  |_  [top=@ bot=@]
```

16-bit rotator core

    ~zod/try=> ~(. mu 0x20e5 0x5901)
    <3.sjm [[@ux @ux] <414.hhh 100.xkc 1.ypj %164>]>

###++zag

```
  ++  zag  [p=(end 4 1 (add top bot)) q=bot]
```

Add bottom into top

    ~zod/try=> `[@ux @ux]`~(zag mu 0x20e0 0x201)
    [0x22e1 0x201]

###++zig

```
  ++  zig  [p=(end 4 1 (add top (sub 0x1.0000 bot))) q=bot]
```

Subtract bottom out of top

    ~zod/try=> `[@ux @ux]`~(zig mu 0x2f46 0x1042)
    [0x1f04 0x1042]
    
###++zug

```
  ++  zug  (mix (lsh 4 1 top) bot)
  --
::
```

Concat into atom

    ~zod/try=> `@ux`~(zug mu 0x10e1 0xfa)
    0x10e1.00fa

###++so

```
++  so
  |%
```

Coin parsing core.

    ~zod/try=> so
    <10.mkn 414.hhh 100.xkc 1.ypj %164>

###++bisk

```
  ++  bisk
    ;~  pose
      ;~  pfix  (just '0')
        ;~  pose
          (stag %ub ;~(pfix (just 'b') bay:ag))
          (stag %ui ;~(pfix (just 'i') dim:ag))
          (stag %ux ;~(pfix (just 'x') hex:ag))
          (stag %uv ;~(pfix (just 'v') viz:ag))
          (stag %uw ;~(pfix (just 'w') wiz:ag))
        ==
      ==
      (stag %ud dem:ag)
    ==
```

Dime parser: numeric literal.

    ~zod/try=> (scan "25" bisk:so)
    [%ud q=25]
    ~zod/try=> (scan "0x12.6401" bisk:so)
    [%ux q=1.205.249]

###++crub

```
  ++  crub
    ;~  pose
      %+  cook
        |=(det=date `dime`[%da (year det)])
      ;~  plug
        %+  cook
          |=([a=@ b=?] [b a])
        ;~(plug dim:ag ;~(pose (cold | hep) (easy &)))
        ;~(pfix dot dim:ag)   ::  month
        ;~(pfix dot dim:ag)   ::  day
        ;~  pose
          ;~  pfix
            ;~(plug dot dot)
            ;~  plug
              dum:ag
              ;~(pfix dot dum:ag)
              ;~(pfix dot dum:ag)
              ;~(pose ;~(pfix ;~(plug dot dot) (most dot qix:ab)) (easy ~))
            ==
          ==
          (easy [0 0 0 ~])
        ==
      ==
    ::
      %+  cook
        |=  [a=(list ,[p=?(%d %h %m %s) q=@]) b=(list ,@)]
        =+  rop=`tarp`[0 0 0 0 b]
        |-  ^-  dime
        ?~  a
          [%dr (yule rop)]
        ?-  p.i.a
          %d  $(a t.a, d.rop (add q.i.a d.rop))
          %h  $(a t.a, h.rop (add q.i.a h.rop))
          %m  $(a t.a, m.rop (add q.i.a m.rop))
          %s  $(a t.a, s.rop (add q.i.a s.rop))
        ==
      ;~  plug
        %+  most
          dot
        ;~  pose
          ;~(pfix (just 'd') (stag %d dim:ag))
          ;~(pfix (just 'h') (stag %h dim:ag))
          ;~(pfix (just 'm') (stag %m dim:ag))
          ;~(pfix (just 's') (stag %s dim:ag))
        ==
        ;~(pose ;~(pfix ;~(plug dot dot) (most dot qix:ab)) (easy ~))
      ==
    ::
      (stag %p fed:ag)
      ;~(pfix dot (stag %ta urs:ab))
      ;~(pfix sig (stag %t (cook woad urs:ab)))
      ;~(pfix hep (stag %c (cook turf (cook woad urs:ab))))
    ==
```

Dime parser: absolute or relative date, phonetic base, or text

    ~zod/try=> (scan "1926.5.12" crub:so)
    [p=~.da q=170.141.184.449.747.016.871.285.095.307.149.312.000]
    ~zod/try=> (,[%da @da] (scan "1926.5.12" crub:so))
    [%da ~1926.5.12]
    ~zod/try=> (scan "s10" crub:so)
    [p=~.dr q=184.467.440.737.095.516.160]
    ~zod/try=> (,[%dr @dr] (scan "s10" crub:so))
    [%dr ~s10]
    ~zod/try=> (scan "doznec" crub:so)
    [%p 256]
    ~zod/try=> (scan ".mas" crub:so)
    [%ta 7.561.581]

###++nuck

```
  ++  nuck
    %+  knee  *coin  |.  ~+
    %-  stew
    ^.  stet  ^.  limo
    :~  :-  ['a' 'z']  (cook |=(a=@ta [~ %tas a]) sym)
        :-  ['0' '9']  (stag ~ bisk)
        :-  '-'        (stag ~ tash)
        :-  '.'        ;~(pfix dot perd)
        :-  '~'        ;~(pfix sig ;~(pose twid (easy [~ %n 0])))
    ==
```

Coin parser: top level

    ~zod/try=> (scan "~pillyt" nuck:so)
    [% p=[p=~.p q=32.819]]
    ~zod/try=> (scan "0x12" nuck:so)
    [% p=[p=~.ux q=18]]
    ~zod/try=> (scan ".127.0.0.1" nuck:so)
    [% p=[p=~.if q=2.130.706.433]]
    ~zod/try=> `@ud`.127.0.0.1
    2.130.706.433
    ~zod/try=> (scan "._20_0w25_sam__" nuck:so)
    [ %many 
        p
      ~[[% p=[p=~.ud q=20]] [% p=[p=~.uw q=133]] [% p=[p=~.tas q=7.168.371]]]
    ]
    ~zod/try=> `@`%sam
    7.168.371
    ~zod/try=> (scan "~0ph" nuck:so)
    [%blob p=[1 1]]
    ~zod/try=> ~0ph
    [1 1]
    ~zod/try=> `@uv`(jam [1 1])
    0vph


###++nusk

```
  ++  nusk
    (sear |=(a=@ta (rush (wick a) nuck)) urt:ab)
```

Parse singly tuple-literal-escaped coin

    ~zod/try=> ~.asd_a
    ~.asd_a
    ~zod/try=> ._1_~~.asd~-a__
    [1 ~.asd_a]
    ~zod/try=> (scan "~~.asd~-a" nusk:so)
    [% p=[p=~.ta q=418.212.246.369]]
    ~zod/try=> (,[~ %ta @ta] (scan "~~.asd~-a" nusk:so))
    [~ %ta ~.asd_a]

###++perd

```
  ++  perd
    ;~  pose
      (stag ~ zust)
      (stag %many (ifix [cab ;~(plug cab cab)] (more cab nusk)))
    ==
```

Parse . prefixed dime or tuple.

    ~zod/try=> (scan "y" perd:so)
    [~ [%f %.y]]
    ~zod/try=> (scan "n" perd:so)
    [~ [%f %.n]]
    ~zod/try=> |
    %.n
    ~zod/try=> (scan "_20_x__" perd:so)
    [%many [[% p=[p=~.ud q=20]] ~[[% p=[p=~.tas q=120]]]]]

###++royl

```
  ++  royl
    =+  ^=  zer
        (cook lent (star (just '0')))
    =+  ^=  voy
        %+  cook  royl-cell
        ;~  plug
          ;~(pose (cold | hep) (easy &))
          ;~(plug dim:ag ;~(pose ;~(pfix dot ;~(plug zer dim:ag)) (easy [0 0])))
          ;~  pose 
            ;~  pfix 
              (just 'e') 
              (cook some ;~(plug ;~(pose (cold | hep) (easy &)) dim:ag))
            == 
            (easy ~)  
          ==
        ==
    ;~  pose
      (stag %rh (cook rylh ;~(pfix ;~(plug sig sig) voy)))
      (stag %rq (cook rylq ;~(pfix ;~(plug sig sig sig) voy)))
      (stag %rd (cook ryld ;~(pfix sig voy)))
      (stag %rs (cook ryls voy)
    ==
```

Dime parser: float

    /~zod/try=> (scan "~3.14" royl:so)
    [%rd .~3.13999999999999]
    /~zod/try=> .~3.14
    .~3.13999999999999

###++royl-cell

```
  ++  royl-cell
    |=  [a=? b=[c=@ d=@ e=@] f=(unit ,[h=? i=@])]  
    ^-  [? @ @ @ (unit ,@s)]
    ?~  f
      [a c.b d.b e.b ~]
    ?:  h.u.f
      [a c.b d.b e.b [~ (mul i.u.f 2)]]
    [a c.b d.b e.b [~ (dec (mul i.u.f 2))]]
```

Intermediate parsed float convereter

###++tash

```
  ++  tash
    =+  ^=  neg
        |=  [syn=? mol=dime]  ^-  dime
        ?>  =('u' (end 3 1 p.mol))
        [(cat 3 's' (rsh 3 1 p.mol)) (new:si syn q.mol)]
    ;~  pfix  hep
      ;~  pose
        (cook |=(a=dime (neg | a)) bisk)
        ;~(pfix hep (cook |=(a=dime (neg & a)) bisk))
      ==
    ==
```

Dime parser: signed

    ~zod/try=> (scan "-20" tash:so)
    [p=~.sd q=39]
    ~zod/try=> (,[%sd @sd] (scan "-20" tash:so))
    [%sd -20]
    ~zod/try=> (,[%sd @sd] (scan "--20" tash:so))
    [%sd --20]
    ~zod/try=> (,[%sx @sx] (scan "--0x2e" tash:so))
    [%sx --0x2e]


###++twid

```
  ++  twid
    ;~  pose
      (cook |=(a=@ [%blob (cue a)]) ;~(pfix (just '0') vum:ag))
      (stag ~ crub)
    ==
  ::
```

Parse ~ prefixed coin: base32 jam-noun or dime.

    ~zod/try=> (scan "zod" twid:so)
    [~ [%p 0]]
    ~zod/try=> (scan ".sam" twid:so)
    [~ [%ta 7.168.371]]
    ~zod/try=> `@ud`~.sam
    7.168.371
    ~zod/try=> `@t`~.sam
    'sam'
    ~zod/try=> (scan "0ph" twid:so)
    [%blob [1 1]]


###++zust

```
  ++  zust
    ;~  pose
      (stag %is bip:ag)
      (stag %if lip:ag)
      (stag %f ;~(pose (cold & (just 'y')) (cold | (just 'n'))))
      royl
    ==
  --
```

Parse . prefixed dime: ip adress, loobean, or float.

    ~zod/try=> (scan "127.0.0.1" zust:so)
    [%if q=2.130.706.433]
    ~zod/try=> (scan "af.0.0.0.0.e7a5.30d2.7" zust:so)
    [%is q=908.651.950.243.594.834.993.091.554.288.205.831]
    ~zod/try=> (,[%is @is] (scan "af.0.0.0.0.e7a5.30d2.7" zust:so))
    [%is .af.0.0.0.0.e7a5.30d2.7]
    ~zod/try=> (,[%is @ux] (scan "af.0.0.0.0.e7a5.30d2.7" zust:so))
    [%is 0xaf.0000.0000.0000.0000.e7a5.30d2.0007]
    ~zod/try=> (scan "y" zust:so)
    [%f %.y]
    ~zod/try=> (scan "12.09" zust:so)
    [%rd .~12.00999999999999]

###++scot

```
++  scot  |=(mol=dime ~(rent co %$ mol))
```

Render dime to cord

###++scow

```
++  scow  |=(mol=dime ~(rend co %$ mol))
```

Render dime to tape

###++slat

```
++  slat  |=(mod=@tas |=(txt=@ta (slaw mod txt)))
```

Parse cord to odor partial

###++slav

```
++  slav  |=([mod=@tas txt=@ta] (need (slaw mod txt)))
```

Demand parse cord with odor

###++slaw

```
++  slaw
  |=  [mod=@tas txt=@ta]
  ^-  (unit ,@)
  =+  con=(slay txt)
  ?.(&(?=([~ %$ @ @] con) =(p.p.u.con mod)) ~ [~ q.p.u.con])
::
```

Parse cord with odor

###++slay

```
++  slay
  |=  txt=@ta  ^-  (unit coin)
  =+  vex=((full nuck:so) [[1 1] (trip txt)])
  ?~  q.vex
    ~
  [~ p.u.q.vex]
::
```

Parse cord as coin

###++smyt

```
++  smyt
  |=  bon=path  ^-  tank
  :+  %rose  [['/' ~] ['/' ~] ['/' ~]]
  |-  ^-  (list tank)
  (turn bon |=(a=@ [%leaf (rip 3 a)]))
```

Render path as tank

XX move?
