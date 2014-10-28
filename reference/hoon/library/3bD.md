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

Render path with infix `/`

    ~zod/try=> `@t`(moon /image/png)
    'image/png'
    ~zod/try=> `@t`(moon /text/x-hoon)
    'text/x-hoon'
    ~zod/try=> `@t`(moon /application/x-pnacl)
    'application/x-pnacl'

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

Parser generator: finite list of term options.

    ~zod/try=> (scan "ham" (perk %sam %ham %lam ~))
    %ham
    ~zod/try=> (scan "ram" (perk %sam %ham %lam ~))
    ! {1 1}
    ! exit


###++poja

```
++  poja                                                ::  parse JSON
  |%
```

JSON parser core

    ~zod/try=> poja
    <21.svd 250.qyy 41.jdd 373.unk 100.kzl 1.ypj %164>

###++apex

```
   ++  apex  ;~(pose abox obox)                          ::  JSON object
```

Top level: a JSON is an array or an object.

    ~zod/try=> (rash '[1,2]' apex:poja)
    [%a p=~[[%n p=~.1] [%n p=~.2]]]
    ~zod/try=> (rash '{"sam": "kot"}' apex:poja)
    [%o p={[p=~.sam q=[%s p=~.kot]]}]
    ~zod/try=> (rash 'null' apex:poja)
    ! {1 1}
    ! exit

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
```

Value: a JSON value is a null, boolean, string, number, array, or object.

    ~zod/try=> (rash '[1,2]' valu:poja)
    [%a p=~[[%n p=~.1] [%n p=~.2]]]
    ~zod/try=> (rash '{"sam": "kot"}' valu:poja)
    [%o p={[p='sam' q=[%s p=~.kot]]}]
    ~zod/try=> (rash 'null' valu:poja)
    ~
    ~zod/try=> (rash '20' valu:poja)
    [%n p=~.20]
    ~zod/try=> (rash '"str"' valu:poja)
    [%s p=~.str]
    ~zod/try=> (rash 'true' valu:poja)
    [%b p=%.y]
   
##JSON arrays

###++abox

```
  ++  abox  (stag %a (ifix [sel (ws ser)] (more (ws com) valu)))
```

Array: values in `[]` separated by `,`

    ~zod/try=> (rash '[1, 2,4]' abox:poja)
    [[%n p=~.1] ~[[%n p=~.2] [%n p=~.4]]]

##JSON Objects

###++pair

```
  ++  pair  ;~(plug ;~(sfix (ws stri) (ws col)) valu)
```

Key-value pair: string and value delimited by `:`

    ~zod/try=> (rash '"ham": 2' pair:poja)
    ['ham' [%n p=~.2]]

###++obje

```
  ++  obje  (ifix [(ws kel) (ws ker)] (more (ws com) pair))
```

Object: pairs in `{}` separated by `,`

    ~zod/try=> (rash '{"ham": 2, "lam":true}' obje:poja)
    [['ham' [%n p=~.2]] ~[['lam' [%b p=%.y]]]]

###++obox

```
  ++  obox  (stag %o (cook mo obje))
```

Boxed object: map with a tag of `%o`.

    ~zod/try=> (rash '{"ham": 2, "lam":true}' obox:poja)
    [%o {[p='lam' q=[%b p=%.y]] [p='ham' q=[%n p=~.2]]}]

##JSON Booleans

###++bool

```
  ++  bool  ;~(pose (cold & (jest 'true')) (cold | (jest 'false')))
```

Boolean: `true` or `false`

    ~zod/try=> (rash 'true' bool:poja)
    %.y
    ~zod/try=> (rash 'false' bool:poja)
    %.n
    ~zod/try=> (rash 'null' bool:poja)
    ! {1 1}
    ! exit

##JSON strings

###++stri

```
  ++  stri
    (cook crip (ifix [doq doq] (star jcha)))
```

String: characters in double quotes, backslashes escaping. 

    ~zod/try=> (rash '"ham"' stri:poja)
    'ham'
    ~zod/try=> (rash '"h\\nam"' stri:poja)
    'h
      am'
    ~zod/try=> (rash '"This be \\"quoted\\""' stri:poja)
    'This be "quoted"'

###++jcha

```
 ++  jcha  ;~(pose ;~(less doq bas prn) esca)           :: character in string
```

Character: literal or escaped

    ~zod/try=> (rash 'a' jcha:poja)
    'a'
    ~zod/try=> (rash '!' jcha:poja)
    '!'
    ~zod/try=> (rash '\\"' jcha:poja)
    '"'
    ~zod/try=> (rash '\\u00a4' jcha:poja)
    '¤'
    ~zod/try=> (rash '\\n' jcha:poja)
    '
     '


###++esca

```
  ++  esca                                               :: Escaped character
    ;~  pfix  bas
      ;~  pose
        doq  fas  soq  bas
        (sear ~(get by `(map ,@t ,@)`(mo b/8 t/9 n/10 f/12 r/13 ~)) low)
        ;~(pfix (just 'u') (cook tuft qix:ab))           :: 4-digit hex to UTF-8
      ==
```

Backslash escaped special character, low ASCII, or UTF16 codepoint

    ~zod/try=> (rash 'b' esca:poja)
    ! {1 1}
    ! exit
    ~zod/try=> (rash '\n' esca:poja)
    ~ <syntax error at [1 9]>
    ~zod/try=> (rash '\\n' esca:poja)
    '
     '
    ~zod/try=> `@`(rash '\\r' esca:poja)
    13
    ~zod/try=> (rash '\\u00c4' esca:poja)
    'Ä'
    ~zod/try=> (rash '\\u00df' esca:poja)
    'ß'

##JSON numbers

###++numb

```
  ++  numb
    ;~  (comp twel)
      (mayb (piec hep))
      ;~  pose
        (piec (just '0'))
        ;~(plug (shim '1' '9') digs)
      ==
      (mayb frac)
      (mayb expo)
    ==
```

Float: optional `-`, decimal number, optional fractional and exponent parts.

    ~zod/try=> (rash '0' numb:poja)
    ~[~~0]
    ~zod/try=> (rash '1' numb:poja)
    ~[~~1]
    ~zod/try=> `tape`(rash '1' numb:poja)
    "1"
    ~zod/try=> `tape`(rash '12.6' numb:poja)
    "12.6"
    ~zod/try=> `tape`(rash '-2e20' numb:poja)
    "-2e20"
    ~zod/try=> `tape`(rash '00e20' numb:poja)
    ! {1 2}
    ! exit


###++digs

```
  ++  digs  (star (shim '0' '9'))
```

Digits: `0` to `9`

    ~zod/try=> (rash '' digs:poja)
    ""
    ~zod/try=> (rash '25' digs:poja)
    "25"
    ~zod/try=> (rash '016' digs:poja)
    "016"
    ~zod/try=> (rash '7' digs:poja)
    "7"

###++expo

```
  ++  expo                                               :: Exponent part
    ;~  (comp twel)
      (piec (mask "eE"))
      (mayb (piec (mask "+-")))
      digs
    ==
```

Exponent part: e, optional `+` or `-`, and digits

    ~zod/try=> `tape`(rash 'e7' expo:poja)
    "e7"
    ~zod/try=> `tape`(rash 'E17' expo:poja)
    "E17"
    ~zod/try=> `tape`(rash 'E-4' expo:poja)
    "E-4"

###++frac

```
  ++  frac   ;~(plug dot digs)                          :: Fractional part
```

Dot followed by digits

    ~zod/try=> (rash '.25' frac:poja)
    [~~~. "25"]
    ~zod/try=> (rash '.016' frac:poja)
    [~~~. "016"]
    ~zod/try=> (rash '.7' frac:poja)
    [~~~. "7"]

##whitespace

###++spac

```
  ++  spac  (star (mask [`@`9 `@`10 `@`13 ' ' ~]))
```

JSON whitespace

    ~zod/try=> (scan "" spac:poja)
    ""
    ~zod/try=> (scan "   " spac:poja)
    "   "
    ~zod/try=> `*`(scan `tape`~[' ' ' ' ' ' `@`9 ' ' ' ' `@`13] spac:poja)
    [32 32 32 9 32 32 13 0]
    ~zod/try=> (scan "   m " spac:poja)
    ! {1 4}
    ! exit


###++ws

```
  ++  ws  |*(sef=_rule ;~(pfix spac sef))
```

Allow whitespace before rule

    ~zod/try=> (rash '   4' digs:poja)
    ! {1 1}
    ! exit
    ~zod/try=> (rash '   4' (ws digs):poja)
    "4"
    ~zod/try=> (rash '''
                     
                     4
                     ''' (ws digs):poja)
    "4"

##plumbing


###++mayb

```
  ++  mayb  |*(bus=_rule ;~(pose bus (easy "")))
```

Optionally parse rule

    ~zod/try=> (abox:poja 1^1 "not-an-array")
    [p=[p=1 q=1] q=~]
    ~zod/try=> ((mayb abox):poja 1^1 "not-an-array")
    [p=[p=1 q=1] q=[~ [p="" q=[p=[p=1 q=1] q="not-an-array"]]]]

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

###++at-raw

```
    ++  at-raw                                            ::  array as tuple
    |*  wil=(pole fist)
    |=  jol=(list json)
    ?~  wil  ~
    :-  ?~(jol ~ (-.wil i.jol))
    ((at-raw +.wil) ?~(jol ~ t.jol))
  ::
```

Parse json array as a tuple of unit results

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

###++ot-raw

```
    ++  ot-raw                                            ::  object as tuple
    |*  wer=(pole ,[cord fist])
    |=  jom=(map ,@t json)
    ?~  wer  ~
    =+  ten=(~(get by jom) -.-.wer)
    [?~(ten ~ (+.-.wer u.ten)) ((ot-raw +.wer) jom)]
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
