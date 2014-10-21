##section 3bD, JSON and XML

###++moon

```
++  moon                                                ::  mime type to text
  |=  myn=mite
  %+  rap
    3
  |-  ^-  tape
  ?~  myn  ~
  ?:  =(~ t.myn)  (trip i.myn)
  (weld (trip i.myn) `tape`['/' $(myn t.myn)])
::
```

XX document

###++perk

```
++  perk                                                ::  pars cube fork
  |*  a=(pole ,@tas)
  ?~  a  fail
  ;~  pose 
    (cold -.a (jest -.a))
    $(a +.a)
  ==
::
```

XX document

###++poja

```
++  poja                                                ::  parse JSON
  |%
```

XX document

###++apex

```
  ++  apex
    =+  spa=;~(pose comt whit)
    %+  knee  *manx  |.  ~+
    %+  ifix  [(star spa) (star spa)]
    ;~  pose
      %+  sear  |=([a=marx b=marl c=mane] ?.(=(c n.a) ~ (some [a b])))
        ;~(plug head (more (star comt) ;~(pose apex chrd)) tail)
      empt
    == 
  :: 
```

XX document

###++valu

```
  ++  valu                                              ::  JSON value
    %+  knee  *json  |.  ~+
    ;~  pfix  spac
      ;~  pose
        (cold ~ (jest 'null'))
        (jify %b bool)
        (jify %s stri)
        (cook |=(s=tape [%n p=(rap 3 s)]) numb)
        abox
        obox
      ==
    ==
  ::  JSON arrays
```

XX document

###++arra

```
  ++  arra  (ifix [sel (ws ser)] (more (ws com) valu))
```

XX document

###++abox

```
  ++  abox  (cook |=(elts=(list json) [%a p=elts]) arra)
  ::  JSON objects
```

XX document

###++pair

```
  ++  pair  ;~((comp |=([k=@ta v=json] [k v])) ;~(sfix (ws stri) (ws col)) valu)
```

XX document

###++obje

```
  ++  obje  (ifix [(ws kel) (ws ker)] (more (ws com) pair))
```

XX document

###++obox

```
  ++  obox  (cook |=(s=(list ,[@ta json]) [%o p=(mo s)]) obje)
  ::  JSON booleans
```

XX document

###++bool

```
  ++  bool  ;~(pose (cold & (jest 'true')) (cold | (jest 'false')))
  ::  JSON strings
```

XX document

###++stri

```
  ++  stri
    (cook |=(s=(list ,@) (rap 3 s)) (ifix [doq doq] (star jcha)))
```

XX document

###++jcha

```
  ++  jcha                                               :: character in string
    ;~  pose
      esca
      ;~  pose
        :: Non-escape string characters
        (shim 32 33)
        (shim 35 91)
        (shim 93 126)
        (shim 128 255)
      ==
    ==
```

XX document

###++esca

```
  ++  esca                                               :: Escaped character
    ;~  pfix  bas
      ;~  pose
        doq
        fas
        soq
        bas
        (cold 8 (just 'b'))
        (cold 9 (just 't'))
        (cold 10 (just 'n'))
        (cold 12 (just 'f'))
        (cold 13 (just 'r'))
        ;~(pfix (just 'u') (cook tuft qix:ab)) :: Convert 4-digit hex to UTF-8
      ==
    ==
  ::  JSON numbers
```

XX document

###++numb

```
  ++  numb
    ;~  (comp twel)
      (mayb (piec hep))
      ;~  pose
        (piec (just '0'))
        ;~((comp twel) (piec (shim '1' '9')) digs)
      ==
      (mayb frac)
      (mayb expo)
    ==
```

XX document

###++digs

```
  ++  digs  (star (shim '0' '9'))
```

XX document

###++expo

```
  ++  expo                                               :: Exponent part
    ;~  (comp twel)
      (piec (mask "eE"))
      (mayb (piec (mask "+-")))
      digs
    ==
```

XX document

###++frac

```
  ++  frac                                               :: Fractional part
    ;~  (comp twel)
      (piec dot)
      digs
    ==
  ::  whitespace
```

XX document

###++spac

```
  ++  spac  (star (mask [`@`9 `@`10 `@`13 ' ' ~]))
```

XX document

###++ws

```
  ++  ws  |*(sef=_rule ;~(pfix spac sef))
  ::  plumbing
```

XX document

###++jify

```
  ++  jify  |*([t=@ta r=_rule] (cook |*([v=*] [t p=v]) r))
```

XX document

###++mayb

```
  ++  mayb  |*(bus=_rule ;~(pose bus (easy "")))
```

XX document

###++twel

```
  ++  twel  |=([a=tape b=tape] (weld a b))
```

XX document

###++piec

```
  ++  piec
    |*  bus=_rule
    (cook |=(a=@ [a ~]) bus)
::
```

XX document

###++pojo

```
++  pojo                                                ::  print json
  |=  val=json
  ^-  tape
  ?~  val  "null"
  ?-    -.val
      %a
    ;:  weld
      "["
      =|  rez=tape
      |-  ^+  rez
      ?~  p.val  rez
      $(p.val t.p.val, rez :(weld rez ^$(val i.p.val) ?~(t.p.val ~ ",")))
      "]"
    ==
 ::
      %b  ?:(p.val "true" "false")
      %n  (trip p.val)
      %s
    ;:  welp
      "\""
      %+  reel
        (turn (trip p.val) jesc)
      |=([p=tape q=tape] (welp +<))
      "\""
    ==
      %o
    ;:  welp
      "\{"
      =+  viz=(~(tap by p.val) ~)
      =|  rez=tape
      |-  ^+  rez
      ?~  viz  rez
      %=    $
          viz  t.viz
          rez
        :(welp rez "\"" (trip p.i.viz) "\":" ^$(val q.i.viz) ?~(t.viz ~ ","))
      ==
      "}"
    ==
  ==
::
```

XX document

###++jo

```
++  jo                                                  ::  json reparser
  =>  |%  ++  grub  (unit ,*) 
          ++  fist  $+(json grub)
  |%
```

Contains converters of ++json to well-typed structures.

A `fist` is a gate that produces some manner of unit from json. Most arms in
`++jo` are fists, or produce them.

###++ar

```
  ++  ar                                                ::  array as list
    |*  wit=fist
    |=  jon=json
    ?.  ?=([%a *] jon)  ~
    %-  zl
    |-  
    ?~  p.jon  ~
    [i=(wit i.p.jon) t=$(p.jon t.p.jon)]
  ::
```

Parse JSON array as typed list.

```
~zod/try=> :type; ((ar ni):jo a/~[n/'1' n/'2'])
[~ u=~[1 2]]
{[%~ u=it(@)] %~}
```

###++at

```
  ++  at                                                ::  array as tuple
    |*  wil=(pole fist)
    |=  jon=json
    ?.  ?=([%a *] jon)  ~
    =+  raw=((at-raw wil) p.jon)
    ?.((za raw) ~ (some (zp raw)))
  ::
```

Parse JSON array as a fixed-length tuple.

```
~zod/try=> :type; ((ar ni):jo a/~[n/'3' s/'to' n/''])
[~ u=[3 'to' 4]]
{[%~ u=[@ @ta @]] %~}
```

###++bo

```
  ++  bo                                                ::  boolean
    |=(jon=json ?.(?=([%b *] jon) ~ [~ u=p.jon]))
  ::
```

Parse JSON boolean.

###++bu

```
  ++  bu                                                ::  boolean not
    |=(jon=json ?.(?=([%b *] jon) ~ [~ u=!p.jon]))
  ::
```

Parse inverse of JSON boolean.

XX  Finish

###++cu

```
  ++  cu                                                ::  transform
    |*  [poq=$+(* *) wit=fist]
    |=  jon=json
    (bind (wit jon) poq)
  ::
```

XX document

###++da

```
  ++  da                                                ::  UTC date
    |=  jon=json
    ?.  ?=([%s *] jon)  ~
    (bind (stud (trip p.jon)) |=(a=date (year a)))
  ::
```

XX document

###++mu

```
  ++  mu                                                ::  true unit
    |*  wit=fist
    |=  jon=json
    ?~(jon (some ~) (wit jon))
  ::
```

XX document

###++ne

```
  ++  ne                                                ::  number as real
    |=  jon=json
    ^-  (unit ,@rd)
    !!
  ::
```

XX document

###++ni

```
  ++  ni                                                ::  number as integer
    |=  jon=json 
    ?.  ?=([%n *] jon)  ~
    (slaw %ui (cat 3 '0i' p.jon))
  ::
```

XX document

###++no

```
  ++  no                                                ::  number as cord
    |=  jon=json
    ?.  ?=([%n *] jon)  ~
    (some p.jon)
  ::
```

XX document

###++of

```
  ++  of                                                ::  object as frond
    |*  wer=(pole ,[cord fist])
    |=  jon=json
    ?.  ?=([%o [@ *] ~ ~] jon)  ~
    |-
    ?~  wer  ~
    ?:  =(-.-.wer p.n.p.jon)  
      ((pe -.-.wer +.-.wer) q.n.p.jon)
    ((of +.wer) jon)
  ::
```

XX document

###++ot

```
  ++  ot                                                ::  object as tuple
    |*  wer=(pole ,[cord fist])
    |=  jon=json
    ?.  ?=([%o *] jon)  ~
    =+  raw=((ot-raw wer) p.jon)
    ?.((za raw) ~ (some (zp raw)))
  ::
```

XX document

###++ot

```
  ++  ot                                                ::  object as tuple
    |*  wer=(pole ,[cord fist])
    |=  jon=json
    ?.  ?=([%o *] jon)  ~
    =+  raw=((ot-raw wer) p.jon)
    ?.((za raw) ~ (some (zp raw)))
  ::
```

XX document

###++om

```
  ++  om                                                ::  object as map
    |*  wit=fist
    |=  jon=json
    ?.  ?=([%o *] jon)  ~
    %-  zm
    |-  
    ?~  p.jon  ~
    [n=[p=p.n.p.jon q=(wit q.n.p.jon)] l=$(p.jon l.p.jon) r=$(p.jon r.p.jon)]
  ::
```

XX document

###++pe

```
  ++  pe                                                ::  prefix
    |*  [pre=* wit=fist]
    (cu |*(a=* [pre a]) wit)
  ::
```

XX document

###++sa

```
  ++  sa                                                ::  string as tape
    |=  jon=json
    ?.(?=([%s *] jon) ~ (some (trip p.jon)))
  ::
```

XX document

###++so

```
  ++  so                                                ::  string as cord
    |=  jon=json
    ?.(?=([%s *] jon) ~ (some p.jon))
  ::
```

XX document

###++su

```
  ++  su                                                ::  parse string
    |*  sab=rule
    |=  jon=json
    ?.  ?=([%s *] jon)  ~
    (rush p.jon sab)
  ::
```

XX document

###++ul

```
  ++  ul  |=(jon=json ?~(jon (some ~) ~))               ::  null
```

XX document

###++za

```
  ++  za                                                ::  full unit pole
    |*  pod=(pole (unit))
    ?~  pod  &
    ?~  -.pod  |
    (za +.pod)
  ::
```

XX document

###++zl

```
  ++  zl                                                ::  collapse unit list
    |*  lut=(list (unit))
    ?.  |-  ^-  ?
        ?~(lut & ?~(i.lut | $(lut t.lut)))
      ~
    %-  some
    |-
    ?~  lut  ~
    [i=u:+.i.lut t=$(lut t.lut)]
  ::
```

XX document

###++zp

```
  ++  zp                                                ::  unit tuple
    |*  but=(pole (unit))
    ?~  but  !!
    ?~  +.but  
      u:->.but
    [u:->.but (zp +.but)]
  ::
```

XX document

###++zt

```
  ++  zt                                                ::  unit tuple
    |*  lut=(list (unit))
    ?:  =(~ lut)  ~
    ?.  |-  ^-  ?
        ?~(lut & ?~(i.lut | $(lut t.lut)))
      ~
    %-  some
    |-
    ?~  lut  !!
    ?~  t.lut  u:+.i.lut
    [u:+.i.lut $(lut t.lut)]
  ::
```

XX document

###++zm

```
  ++  zm                                                ::  collapse unit map
    |*  lum=(map term (unit))
    ?.  |-  ^-  ?
        ?~(lum & ?~(q.n.lum | &($(lum l.lum) $(lum r.lum))))
      ~
    %-  some
    |-
    ?~  lum  ~
    [[p.n.lum u:+.q.n.lum] $(lum l.lum) $(lum r.lum)]
::
```

XX document

###++joba

```
++  joba
  |=  [p=@t q=json]
  ^-  json
  [%o [[p q] ~ ~]]
::
```

XX document

###++jobe

```
++  jobe
  |=  a=(list ,[p=@t q=json])
  ^-  json
  [%o (~(gas by *(map ,@t json)) a)]
::
```

XX document

###++jape

```
++  jape
  |=  a=tape
  ^-  json
  [%s (crip a)]
::
```

XX document

###++jone

```
++  jone
  |=  a=@
  ^-  json
  :-  %n
  ?:  =(0 a)  '0'
  (crip (flop |-(^-(tape ?:(=(0 a) ~ [(add '0' (mod a 10)) $(a (div a 10))])))))
::
```

XX document

###++jesc

```
++  jesc
  |=  a=@  ^-  tape
  ?+  a  [a ~]
    10  "\\n"
    34  "\\\""
    92  "\\\\"
  ==
::
```

XX document

###++scanf

```
++  scanf                                              ::  formatted scan
  |*  [tape (pole ,_:/(*$&(_rule tape)))]
  =>  .(+< [a b]=+<)
  (scan a (parsf b))
```

Scan with `;"`-interpolated parsers.

```
~zod/try=> `[p=@ud q=@ud]`(scanf "Score is 5 to 2" [;"Score is {n} to {n}"]:n=dim:ag)
[p=5 q=2]
```

```
~zod/try=> =n ;~(pfix (star (just '0')) (cook |=(@ud +<) dim:ag))
~zod/try=> (scanf "2014-08-12T23:10:58.931Z" ;"{n}\-{n}\-{n}T{n}:{n}:{n}.{n}Z")
[2.014 8 12 23 10 58 931]
~zod/try=> =dat (scanf "2014-08-12T23:10:58.931Z" ;"{n}\-{n}\-{n}T{n}:{n}:{n}.{n}Z")
~zod/try=> `@da`(year `date`dat(- [%& -.dat], |6 ~[(div (mul |6.dat (bex 16)) 1.000)]))
~2014.8.12..23.10.58..ee56
```

###++parsf

```
++  parsf                                              ::  make parser from:
  |^  |*  a=(pole ,_:/(*$&(_rule tape)))               ::  ;"chars{rule}chars"
      %-  cook  :_  (bill (norm a))
      |*  (list)
      ?~  +<  ~
      ?~  t  i
      [i $(+< t)]
  ::
  ::  .=  (norm [;"{n}, {n}"]:n=dim:ag)  ~[[& dim] [| ", "] [& dim]]:ag
```

`parsf` generates a `_rule` from a tape with rules embedded in it, literal
sections being matched verbatim. The parsed type is a tuple of the embedded
rules' results.

Two intermediate arms are used:

####++norm

```
  ++  norm                                             
    |*  (pole ,_:/(*$&(_rule tape)))
    ?~  +<  ~
    =>  .(+< [i=+<- t=+<+])
    :_  t=$(+< t)
    =+  rul=->->.i
    ^=  i
    ?~  rul     [%| p=rul]
    ?~  +.rul   [%| p=rul]
    ?@  &2.rul  [%| p=;;(tape rul)]
    [%& p=rul]
  ::
  ::  .=  (bill ~[[& dim] [| ", "] [& dim]]:ag)
  ::  ;~(plug dim ;~(pfix com ace ;~(plug dim (easy)))):ag
```

`norm` converts a `;"` pole of `[[%~. [%~. ?(tape _rule)] ~] ~]` into a more
convenient list of discriminated tapes and rules.

####++bill

```
  ++  bill
    |*  (list (each ,_rule tape))
    ?~  +<  (easy ~)
    ?:  ?=(| -.i)  ;~(pfix (jest (crip p.i)) $(+< t))
    %+  cook  |*([* *] [i t]=+<)
    ;~(plug p.i $(+< t))
::
```

`bill` builds a parser out of rules and tapes, ignoring the literal sections
and producing a list of the rules' results.

###++taco

```
++  taco                                                ::  atom to octstream
  |=  tam=@  ^-  octs
  [(met 3 tam) tam]
::
```

XX document

###++tact

```
++  tact                                                ::  tape to octstream
  |=  tep=tape  ^-  octs
  (taco (rap 3 tep))
::
```

XX document

###++tell

```
++  tell                                                ::  wall to octstream
  |=  wol=wall  ^-  octs
  =+  buf=(rap 3 (turn wol |=(a=tape (crip (weld a `tape`[`@`10 ~])))))
  [(met 3 buf) buf]
::
```

XX document

###++txml

```
++  txml                                                ::  string to xml
  |=  tep=tape  ^-  manx
  [[%$ [%$ tep] ~] ~]
::
```

XX document

###++xmla

```
++  xmla                                                ::  attributes to tape
  |=  [tat=mart rez=tape]
  ^-  tape
  ?~  tat  rez
  =+  ryq=$(tat t.tat)
  :(weld (xmln n.i.tat) "=\"" (xmle | v.i.tat '"' ?~(t.tat ryq [' ' ryq])))
::
```

XX document

###++xmle

```
++  xmle                                                ::  escape for xml
  |=  [unq=? tex=tape rez=tape]
  ?:  unq
    (weld tex rez)
  =+  xet=`tape`(flop tex)
  |-  ^-  tape
  ?~  xet  rez
  %=    $
    xet  t.xet
    rez  ?-  i.xet
           34  ['&' 'q' 'u' 'o' 't' ';' rez]
           38  ['&' 'a' 'm' 'p' ';' rez]
           39  ['&' '#' '3' '9' ';' rez]
           60  ['&' 'l' 't' ';' rez]
           62  ['&' 'g' 't' ';' rez]
           *   [i.xet rez]
         ==
  ==
::
```

XX document

###++xmln

```
++  xmln                                                ::  name to tape
  |=  man=mane  ^-  tape
  ?@  man  (trip man)
  (weld (trip -.man) `tape`[':' (trip +.man)])
::
```

XX document

###++xmll

```
++  xmll                                                ::  nodelist to tape
  |=  [unq=? lix=(list manx) rez=tape]
  |-  ^-  tape
  ?~  lix  rez
  (xmlt unq i.lix $(lix t.lix))
::
```

XX document

###++xmlt

```
++  xmlt                                                ::  node to tape
  |=  [unq=? mex=manx rez=tape]
  ^-  tape
  ?:  ?=([%$ [[%$ *] ~]] g.mex)
    (xmle unq v.i.a.g.mex rez)
  =+  man=`mane`-.g.mex
  =.  unq  |(unq =(%script man) =(%style man))
  =+  tam=(xmln man)
  =+  end=:(weld "</" tam ">" rez)
  =+  bod=['>' (xmll unq c.mex :(weld "</" tam ">" rez))]
  =+  att=`mart`a.g.mex
  :-  '<'
  %+  weld  tam
  `_tam`?~(att bod [' ' (xmla att bod)])
::
```

XX document

###++xmlp

```
++  xmlp                                                ::  xml parser
  |%
```

XX document

###++apex

```
  ++  apex
    =+  spa=;~(pose comt whit)
    %+  knee  *manx  |.  ~+
    %+  ifix  [(star spa) (star spa)]
    ;~  pose
      %+  sear  |=([a=marx b=marl c=mane] ?.(=(c n.a) ~ (some [a b])))
        ;~(plug head (more (star comt) ;~(pose apex chrd)) tail)
      empt
    == 
  :: 
```

XX document

###++attr

```
  ++  attr                                              ::  attribute
    %+  knee  *mart  |.  ~+ 
    %-  star
    ;~  pfix  (plus whit)
      ;~  plug  name  
        ;~  pfix  tis
          ;~  pose 
              (ifix [doq doq] (star ;~(less doq escp)))
              (ifix [soq soq] (star ;~(less soq escp)))
          ==  
        ==
      ==  
    ==
  ::
```

XX document

###++chrd

```
  ++  chrd                                              ::  character data
    %+  knee  *manx  |.  ~+
    %+  cook  |=(a=tape :/(a))
    (plus ;~(less soq doq ;~(pose (just `@`10) escp)))
  ::
```

XX document

###++comt

```
  ++  comt  %+  ifix  [(jest '<!--') (jest '-->')]      ::  comments 
            (star ;~(less (jest '-->') ;~(pose whit prn)))
  ::
```

XX document

###++escp

```
  ++  escp
    ;~  pose
      ;~(less gal gar pam prn)
      (cold '>' (jest '&gt;'))
      (cold '<' (jest '&lt;'))
      (cold '&' (jest '&amp;'))
      (cold '"' (jest '&quot;'))
      (cold '\'' (jest '&apos;'))
    ==
```

XX document

###++empt

```
  ++  empt                                              ::  self-closing tag
    %+  ifix  [gal ;~(plug (stun [0 1] ace) (jest '/>'))] 
    ;~(plug ;~(plug name attr) (cold ~ (star whit)))  
  ::
```

XX document

###++head

```
  ++  head                                              ::  opening tag
    %+  knee  *marx  |.  ~+
    (ifix [gal gar] ;~(plug name attr))
  ::
```

XX document

###++name

```
  ++  name                                              ::  tag name 
    %+  knee  *mane  |.  ~+
    =+  ^=  chx
        %+  cook  crip 
        ;~  plug 
            ;~(pose cab alf) 
            (star ;~(pose cab dot alp))
        ==
    ;~(pose ;~(plug ;~(sfix chx col) chx) chx)
  ::
```

XX document

###++tail

```
  ++  tail  (ifix [(jest '</') gar] name)               ::  closing tag
```

XX document

###++whit

```
  ++  whit  (mask ~[`@`0x20 `@`0x9 `@`0xa])             ::  whitespace
::
```

XX document
