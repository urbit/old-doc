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
  =<  |=(a=cord (rush a apex))
  |%
```

JSON parser core

    ~zod/try=> (poja '[1,2,3]')
    [~ [%a p=~[[%n p=~.1] [%n p=~.2] [%n p=~.3]]]]
    ~zod/try=> (poja 'null')
    [~ ~]
    ~zod/try=> (poja 'invalid{json')
    ~


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

Weld two tapes

    ~zod/try=> (twel "sam" "hok"):poja
    ~[~~s ~~a ~~m ~~h ~~o ~~k]
    ~zod/try=> (twel "kre" ""):poja
    ~[~~k ~~r ~~e]


###++piec

```
  ++  piec
    |*  bus=_rule
    (cook |=(a=@ [a ~]) bus)
::
```

Piece to list

    ~zod/try=> (scan "4" (piec:poja dem:ag))
    [4 ~]

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

Print JSON to tape

    ~zod/try=> (pojo [%n '12.6'])
    "12.6"
    ~zod/try=> (crip (pojo %n '12.6'))
    '12.6'
    ~zod/try=> (crip (pojo %s 'samtel'))
    '"samtel"'
    ~zod/try=> (crip (pojo %a ~[(jone 12) (jape "ha")]))
    '[12,"ha"]'
    ~zod/try=> (crip (pojo %a ~[(jone 12) ~ (jape "ha")]))
    '[12,null,"ha"]'
    ~zod/try=> (crip (pojo %o (mo sale/(jone 12) same/b/| ~)))
    '{"same":false,"sale":12}'
    
###++poxo

```
++  poxo                                                ::  node to tape
  =<  |=(a=manx `tape`(apex a ~))
  |_  unq=?                                             ::  unq
```

Print xml

    ~zod/try=> (poxo ;div;)
    "<div></div>"
    ~zod/try=> (poxo ;div:(p a))
    "<div><p></p><a></a></div>"
    ~zod/try=> (poxo ;div:(p:"tree > text" a))
    "<div><p>tree &gt; text</p><a></a></div>"

###++apex

```
  ++  apex                                              ::  top level
    |=  [mex=manx rez=tape]
    ^-  tape
    ?:  ?=([%$ [[%$ *] ~]] g.mex)
      (escp v.i.a.g.mex rez)
    =+  man=`mane`n.g.mex
    =.  unq  |(unq =(%script man) =(%style man))
    =+  tam=(name man)
    =.  rez  :(weld "</" tam ">" rez)
    =+  att=`mart`a.g.mex
    :-  '<'
    %+  welp  tam
    =.  rez  ['>' (many c.mex rez)]
    ?~(att rez [' ' (attr att rez)])
  ::  
```

Inner XML printer

    ~zod/try=> (apex:poxo ;div; "")
    "<div></div>"
    ~zod/try=> (apex:poxo ;div:(p a) "")
    "<div><p></p><a></a></div>"
    ~zod/try=> (apex:poxo ;div:(p:"tree > text" a) "")
    "<div><p>tree &gt; text</p><a></a></div>"
    ~zod/try=> (~(apex poxo &) ;div:(p:"tree > text" a) "")
    "<div><p>tree > text</p><a></a></div>"
    
###++attr

```
  ++  attr                                              ::  attributes to tape
    |=  [tat=mart rez=tape]
    ^-  tape
    ?~  tat  rez
    =.  rez  $(tat t.tat)
    ;:  weld 
      (name n.i.tat)
      "=\"" 
      (escp(unq |) v.i.tat '"' ?~(t.tat rez [' ' rez]))
    ==
```

Render XML attributes

    ~zod/try=> (attr:poxo ~ "")
    ""
    ~zod/try=> (crip (attr:poxo ~[sam/"hem" [%tok %ns]^"reptor"] ""))
    'sam="hem" tok:ns="reptor"'
    ~zod/try=> (crip (attr:poxo ~[sam/"hem" [%tok %ns]^"reptor"] "|appen"))
    'sam="hem" tok:ns="reptor"|appen'

###++escp

```
  ++  escp                                              ::  escape for xml
    |=  [tex=tape rez=tape]
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

Escape xml entities

    ~zod/try=> (escp:poxo "astra" ~)
    ~[~~a ~~s ~~t ~~r ~~a]
    ~zod/try=> `tape`(escp:poxo "astra" ~)
    "astra"
    ~zod/try=> `tape`(escp:poxo "x > y" ~)
    "x &gt; y"
    ~zod/try=> `tape`(~(escp poxo &) "x > y" ~)
    "x > y"

###++name

```
  ++  name                                              ::  name to tape
    |=  man=mane  ^-  tape
    ?@  man  (trip man)
    (weld (trip -.man) `tape`[':' (trip +.man)])
  ::
```

Render `mane`

    ~zod/try=> (name:poxo %$)
    ""
    ~zod/try=> (name:poxo %ham)
    "ham"
    ~zod/try=> (name:poxo %ham^%tor)
    "ham:tor"

###++many

```
  ++  many                                              ::  nodelist to tape
    |=  [lix=(list manx) rez=tape]
    |-  ^-  tape
    ?~  lix  rez
    (apex i.lix $(lix t.lix))
  ::
```

Multiple XML nodes to tape

    ~zod/try=> (many:poxo ~ "")
    ""
    ~zod/try=> (many:poxo ;"hare" "")
    "hare"
    ~zod/try=> (many:poxo ;"hare;{lep}ton" "")
    "hare<lep></lep>ton"
    ~zod/try=> ;"hare;{lep}ton"
    [[[%~. [%~. "hare"] ~] ~] [[%lep ~] ~] [[%~. [%~. "ton"] ~] ~] ~]

---

###++poxa

```
++  poxa                                                ::  xml parser
  =<  |=(a=cord (rush a apex))
  |%
```

Parse xml

    ~zod/try=> (poxa '<div />')
    [~ [g=[n=%div a=~] c=~]]
    ~zod/try=> (poxa '<html><head/> <body/></html>')
    [~ [g=[n=%html a=~] c=~[[g=[n=%head a=~] c=~] [g=[n=%body a=~] c=~]]]]
    ~zod/try=> (poxa '<script src="/gep/hart.js"/>')
    [~ [g=[n=%script a=~[[n=%src v="/gep/hart.js"]]] c=~]]
    ~zod/try=> (poxa '<<<<')
    ~


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

Top level parser

    ~zod/try=> (rash '<div />' apex:xmlp)
    [g=[n=%div a=~] c=~]
    ~zod/try=> (rash '<html><head/> <body/></html>' apex:xmlp)
    [g=[n=%html a=~] c=~[[g=[n=%head a=~] c=~] [g=[n=%body a=~] c=~]]]
    ~zod/try=> (rash '<script src="/gep/hart.js"/>' apex:xmlp)
    [g=[n=%script a=~[[n=%src v="/gep/hart.js"]]] c=~]
    ~zod/try=> (rash '<<<<' apex:xmlp)
    ! {1 2}
    ! exit


###++attr

```
  ++  attr                                              ::  attributes
    %+  knee  *mart  |.  ~+ 
    %-  star
    ;~  plug
        ;~(sfix name tis)
        ;~  pose 
            (ifix [doq doq] (star ;~(less doq escp)))
            (ifix [soq soq] (star ;~(less soq escp)))
        ==
      ==  
  ::
```

0 or more . gap [mane] tis {quoted string}

    ~zod/try=> (rash '' attr:xmlp)
    ~
    ~zod/try=> (rash 'sam=""' attr:xmlp)
    ! {1 1}
    ! exit
    ~zod/try=> (rash ' sam=""' attr:xmlp)
    ~[[n=%sam v=""]]
    ~zod/try=> (rash ' sam="hek"' attr:xmlp)
    ~[[n=%sam v="hek"]]
    ~zod/try=> (rash ' sam="hek" res="actor"' attr:xmlp)
    ~[[n=%sam v="hek"] [n=%res v="actor"]]
    ~zod/try=> (rash ' sam=\'hek\' res="actor"' attr:xmlp)
    ~[[n=%sam v="hek"] [n=%res v="actor"]]
    ~zod/try=> (rash ' sam=\'hek" res="actor"' attr:xmlp)
    ! {1 23}
    ! exit

###++chrd

```
  ++  chrd                                              ::  character data
    %+  cook  |=(a=tape ^-(mars :/(a)))
    (plus ;~(less soq doq ;~(pose (just `@`10) escp)))
  ::
```

Char data

    ~zod/try=> (rash 'asa' chrd:xmlp)
    [g=[n=%$ a=~[[n=%$ v="asa"]]] c=~]
    ~zod/try=> (rash 'asa &gt; are' chrd:xmlp)
    [g=[n=%$ a=~[[n=%$ v="asa > are"]]] c=~]
    ~zod/try=> (rash 'asa > are' chrd:xmlp)
    ! {1 6}
    ! exit

###++comt

```
  ++  comt                                              ::  comments 
    =-  (ifix [(jest '<!--') (jest '-->')] (star -))
    ;~  pose 
      ;~(less hep prn) 
      whit
      ;~(less (jest '-->') hep)
    ==
  ::
```

Comment block

    ~zod/try=> (rash '<!--  bye -->' comt:xmlp)
    "  bye "
    ~zod/try=> (rash '<!--  bye  ><<<>< - - -->' comt:xmlp)
    "  bye  ><<<>< - - "
    ~zod/try=> (rash '<!--  invalid -->-->' comt:xmlp)
    ! {1 18}
    ! exit

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

Nonspecial or escaped character

    ~zod/try=> (rash 'a' escp:xmlp)
    'a'
    ~zod/try=> (rash 'ab' escp:xmlp)
    ! {1 2}
    ! exit
    ~zod/try=> (rash '.' escp:xmlp)
    '.'
    ~zod/try=> (rash '!' escp:xmlp)
    '!'
    ~zod/try=> (rash '>' escp:xmlp)
    ! {1 2}
    ! exit
    ~zod/try=> (rash '&gt;' escp:xmlp)
    '>'
    ~zod/try=> (rash '&quot;' escp:xmlp)
    '"'

###++empt

```
  ++  empt                                              ::  self-closing tag
    %+  ifix  [gal (jest '/>')]  
    ;~(plug ;~(plug name attr) (cold ~ (star whit)))  
  ::
```

XML tags can self-close by ending in `/>`

    ~zod/try=> (rash '<div/>' empt:xmlp)
    [[%div ~] ~]
    ~zod/try=> (rash '<pre color="#eeffee" />' empt:xmlp)
    [[%pre ~[[n=%color v="#eeffee"]]] ~]
    ~zod/try=> (rash '<pre color="#eeffee"></pre>' empt:xmlp)
    ! {1 21}
    ! exit

###++head

```
  ++  head                                              ::  opening tag
    (ifix [gal gar] ;~(plug name attr))
  ::
```

XML node start

    ~zod/try=> (rash '<a>' head:xmlp)
    [n=%a a=~]
    ~zod/try=> (rash '<div mal="tok">' head:xmlp)
    [n=%div a=~[[n=%mal v="tok"]]]
    ~zod/try=> (rash '<div mal="tok" />' head:xmlp)
    ! {1 16}
    ! exit

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

XML node name

    ~zod/try=> (scan "ham" name:xmlp)
    %ham
    ~zod/try=> (scan "ham:tor" name:xmlp)
    [%ham %tor]
    ~zod/try=> (scan "ham-tor" name:xmlp)
    %ham-tor
    ~zod/try=> (scan "ham tor" name:xmlp)
    ! {1 4}
    ! exit

###++tail

```
  ++  tail  (ifix [(jest '</') gar] name)               ::  closing tag
```

`</foo>` closes an xml tag.

    ~zod/try=> (scan "</div>" tail:xmlp)
    %div
    ~zod/try=> (scan "</a>" tail:xmlp)
    %a
    ~zod/try=> (scan "</>" tail:xmlp)
    ! {1 3}
    ! exit

###++whit

```
  ++  whit  (mask ~[' ' `@`0x9 `@`0xa])                 ::  whitespace
::
```

Newlines, tabs, and spaces

    ~zod/try=> `@`(scan " " whit:xmlp)
    32
    ~zod/try=> `@`(scan "  " whit:xmlp)
    ! {1 2}
    ! exit
    ~zod/try=> `@`(scan "\0a" whit:xmlp)
    10
    ~zod/try=> `@`(scan "\09" whit:xmlp)
    9
    ~zod/try=> `@`(scan "\08" whit:xmlp)
    ! {1 1}
    ! exit

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

With fist, parse JSON array as homogenous list.

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

With list of fists, parse JSON array as a fixed-length tuple.

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

Parse list of json as a tuple of unit results

```
~zod/try=> ((at-raw ni ni bo ~):jo ~[s/'hi' n/'1' b/&])
[~ [~ 1] [~ u=%.y] ~]
```

###++bo

```
  ++  bo                                                ::  boolean
    |=(jon=json ?.(?=([%b *] jon) ~ [~ u=p.jon]))
  ::
```

Parse JSON boolean.

```
~zod/try=> (bo:jo [%b &])
[~ u=%.y]
~zod/try=> (bo:jo [%b |])
[~ u=%.n]
~zod/try=> (bo:jo [%s 'hi'])
~
```

###++bu

```
  ++  bu                                                ::  boolean not
    |=(jon=json ?.(?=([%b *] jon) ~ [~ u=!p.jon]))
  ::
```

Parse inverse of JSON boolean.

```
~zod/try=> (bu:jo [%b &])
[~ u=%.n]
~zod/try=> (bu:jo [%b |])
[~ u=%.y]
~zod/try=> (bu:jo [%s 'hi'])
~
```

###++cu

```
  ++  cu                                                ::  transform
    |*  [poq=$+(* *) wit=fist]
    |=  jon=json
    (bind (wit jon) poq)
  ::
```

Slam result through gate.

```
~zod/try=> ((cu dec ni):jo [%n '20'])
[~ 19]
~zod/try=> ((cu dec ni):jo [%b &])
~
```

###++da

```
  ++  da                                                ::  UTC date
    |=  jon=json
    ?.  ?=([%s *] jon)  ~
    (bind (stud (trip p.jon)) |=(a=date (year a)))
  ::
```

Parse UTC date string

```
~zod/try=> (da:jo [%s 'Wed, 29 Oct 2014 0:26:15 +0000'])
[~ ~2014.10.29..00.26.15]
~zod/try=> (da:jo [%s 'Wed, 29 Oct 2012 0:26:15'])
[~ ~2012.10.29..00.26.15]
~zod/try=> (da:jo [%n '20'])
~
```

###++di

```
  ++  di                                                ::  millisecond date
    |=  jon=json
    %+  bind  (ni jon)
    |=  a=@u  ^-  @da
    (add ~1970.1.1 (div (mul ~s1 a) 1.000))
  ::
```

Parse javascript millisecond date integer.

```
~zod/try=> (di:jo [%s '2014-10-29'])
~
~zod/try=> (di:jo [%n '1414545548325'])
[~ ~2014.10.29..01.19.08..5333.3333.3333.3333]
~zod/try=> (di:jo [%n '1414545615128'])
[~ ~2014.10.29..01.20.15..20c4.9ba5.e353.f7ce]
~zod/try=> (di:jo [%n '25000'])
[~ ~1970.1.1..00.00.25]
```

###++mu

```
  ++  mu                                                ::  true unit
    |*  wit=fist
    |=  jon=json
    ?~(jon (some ~) (bind (wit jon) some))
  ::
```

With fist, parse null or some containing that fist.

    ~zod/try=> ((mu ni):jo [%n '20'])
    [~ [~ u=q=20]]
    ~zod/try=> ((mu ni):jo [%n '15'])
    [~ [~ u=q=15]]
    ~zod/try=> ((mu ni):jo ~)
    [~ u=~]
    ~zod/try=> ((mu ni):jo [%s 'ma'])
    ~

###++ne

```
  ++  ne                                                ::  number as real
    |=  jon=json
    ^-  (unit ,@rd)
    !!
  ::
```

XX  Currently unimplemented

###++ni

```
  ++  ni                                                ::  number as integer
    |=  jon=json 
    ?.  ?=([%n *] jon)  ~
    (rush p.jon dem)
  ::
```

Parse integer representation.

    ~zod/try=> (ni:jo [%n '0'])
    [~ q=0]
    ~zod/try=> (ni:jo [%n '200'])
    [~ q=200]
    ~zod/try=> (ni:jo [%n '-2.5'])
    ~
    ~zod/try=> (ni:jo [%s '10'])
    ~
    ~zod/try=> (ni:jo [%b |])
    ~
    ~zod/try=> (ni:jo [%n '4'])
    [~ q=4]
    ~zod/try=> (ni:jo [%a ~[b/& b/& b/& b/&]])
    ~


###++no

```
  ++  no                                                ::  number as cord
    |=  jon=json
    ?.  ?=([%n *] jon)  ~
    (some p.jon)
  ::
```

Retrieve numeric representation as text.

    ~zod/try=> (no:jo [%n '0'])
    [~ u=~.0]
    ~zod/try=> (no:jo [%n '200'])
    [~ u=~.200]
    ~zod/try=> (no:jo [%n '-2.5'])
    [~ u=~.-2.5]
    ~zod/try=> (no:jo [%s '10'])
    ~
    ~zod/try=> (no:jo [%b |])
    ~
    ~zod/try=> (no:jo [%n '4'])
    [~ u=~.4]
    ~zod/try=> (no:jo [%a ~[b/& b/& b/& b/&]])
    ~


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

With list of possible keys and parsers for their values, parse object with one key-value pair

    ~zod/try=> ((of sem/sa som/ni ~):jo %o [%sem s/'hi'] ~ ~)
    [~ [%sem "hi"]]
    ~zod/try=> ((of sem/sa som/ni ~):jo %o [%som n/'20'] ~ ~)
    [~ [%som q=20]]
    ~zod/try=> ((of sem/sa som/ni ~):jo %o [%som s/'he'] ~ ~)
    ~
    ~zod/try=> ((of sem/sa som/ni ~):jo %o [%som s/'5'] ~ ~)
    ~
    ~zod/try=> ((of sem/sa som/ni ~):jo %o [%sem s/'5'] ~ ~)
    [~ [%sem "5"]]
    ~zod/try=> ((of sem/sa som/ni ~):jo %o [%sem n/'2'] ~ ~)
    ~
    ~zod/try=> ((of sem/sa som/ni ~):jo %o [%sem b/&] ~ ~)
    ~
    ~zod/try=> ((of sem/sa som/ni ~):jo %a ~[s/'som' n/'4'])
    ~
    ~zod/try=> ((of sem/sa som/ni ~):jo %o [%sem s/'hey'] ~ [%sam s/'other value'] ~ ~)
    ~


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

With list of keys and fists, parse object with those keys to a tuple of their values

    ~zod/try=> (jobe [%sem s/'ha'] [%som n/'20'] ~)
    [%o p={[p='sem' q=[%s p=~.ha]] [p='som' q=[%n p=~.20]]}]
    ~zod/try=> ((ot sem/sa som/ni sem/sa ~):jo (jobe [%sem s/'ha'] [%som n/'20'] ~))
    [~ u=["ha" q=20 "ha"]]

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

Parse map of cords to json with a list of parsers per key, producing a list of their results

    ~zod/try=> ((ot-raw sem/sa som/ni sem/sa ~):jo (mo [%sem s/'ha'] [%som n/'20'] ~))
    [[~ u="ha"] [~ q=20] [~ u="ha"] ~]
    ~zod/try=> ((ot-raw sem/sa som/ni sem/sa ~):jo (mo [%sem s/'ha'] [%som b/|] ~))
    [[~ u="ha"] ~ [~ u="ha"] ~]

###++om

```
    ++  om                                                ::  object as map
    |*  wit=fist
    |=  jon=json
    ?.  ?=([%o *] jon)  ~
    (zm ~(run by p.jon) wit)
  ::
```

With fist, parse json object to homogenous map

    ~zod/try=> ((om ni):jo (jobe [%sap n/'20'] [%sup n/'5'] [%sop n/'177'] ~))
    [~ {[p='sup' q=q=5] [p='sop' q=q=177] [p='sap' q=q=20]}]
    ~zod/try=> ((om ni):jo (jobe [%sap n/'20'] [%sup n/'0x5'] [%sop n/'177'] ~))
    ~    

###++pe

```
  ++  pe                                                ::  prefix
    |*  [pre=* wit=fist]
    (cu |*(a=* [pre a]) wit)
  ::
```

Add static prefix to parse result

See also: stag

    ~zod/try=> (ni:jo n/'2')
    [~ q=2]
    ~zod/try=> (ni:jo b/|)
    ~
    ~zod/try=> ((pe %hi ni):jo n/'2')
    [~ [%hi q=2]]
    ~zod/try=> ((pe %hi ni):jo b/|)
    ~


###++sa

```
  ++  sa                                                ::  string as tape
    |=  jon=json
    ?.(?=([%s *] jon) ~ (some (trip p.jon)))
  ::
```

Parse string at char list

    ~zod/try=> (sa:jo s/'value')
    [~ u="value"]
    ~zod/try=> (sa:jo n/'46')
    ~
    ~zod/try=> (sa:jo a/~[s/'val 2'])
    ~


###++so

```
  ++  so                                                ::  string as cord
    |=  jon=json
    ?.(?=([%s *] jon) ~ (some p.jon))
  ::
```

Parse string as LSB atom

    ~zod/try=> (so:jo s/'value')
    [~ u=~.value]
    ~zod/try=> (so:jo n/'46')
    ~
    ~zod/try=> (so:jo a/~[s/'val 2'])
    ~


###++su

```
  ++  su                                                ::  parse string
    |*  sab=rule
    |=  jon=json
    ?.  ?=([%s *] jon)  ~
    (rush p.jon sab)
  ::
```

Apply parsing rule to string

    ~zod/try=> ((su:jo fed:ag) s/'zod')
    [~ 0]
    ~zod/try=> ((su:jo fed:ag) s/'doznec')
    [~ 256]
    ~zod/try=> ((su:jo fed:ag) s/'notship')
    ~
    ~zod/try=> ((su:jo fed:ag) n/'20')
    ~


###++ul

```
  ++  ul  |=(jon=json ?~(jon (some ~) ~))               ::  null
```

Expect null

    ~zod/try=> (ul:jo `json`~)
    [~ u=~]
    ~zod/try=> (ul:jo s/'null')
    ~
    ~zod/try=> (ul:jo b/|)
    ~
    ~zod/try=> (ul:jo b/&)
    ~


###++za

```
  ++  za                                                ::  full unit pole
    |*  pod=(pole (unit))
    ?~  pod  &
    ?~  -.pod  |
    (za +.pod)
  ::
```

Determine if pole of units contains no empty ones. Used internally

    ~zod/try=> (za:jo ~[`1 `2 `3])
    %.y
    ~zod/try=> (za:jo ~[`1 ~ `3])
    %.n

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

Promote unithood: if any elements of a list of units are empty, produce nil,
otherwise produce a full unit containing a list of the contents of the elements.

    ~zod/try=> (zl:jo `(list (unit))`~[`1 `2 `3])
    [~ u=~[1 2 3]]
    ~zod/try=> (zl:jo `(list (unit))`~[`1 `17 `3])
    [~ u=~[1 17 3]]
    ~zod/try=> (zl:jo `(list (unit))`~[`1 ~ `3])
    ~


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

Force collapse pole of units to tuple

    ~zod/try=> (zp:jo `(pole (unit))`~[`1 `2 `3])
    [1 2 3]
    ~zod/try=> (zp:jo `(pole (unit))`~[`1 `17 `3])
    [1 17 3]
    ~zod/try=> (zp:jo `(pole (unit))`~[`1 ~ `3])
    ! exit


###++zm

```
  ++  zm                                                ::  collapse unit map
    |*  lum=(map term (unit))
    ?:  (~(rep by lum) | |=([[@ a=(unit)] b=?] |(b ?=(~ a))))
      ~
    (some (~(run by lum) need))
::
```

If any values in map to units are empty, produce empty, otherwise produce
some of the map with elements promoted.

See also: zp, zl

    ~zod/try=> (zm:jo `(map term (unit ,@u))`(mo a/`4 b/`1 c/`2 ~))
    [~ {[p=%a q=4] [p=%c q=2] [p=%b q=1]}]
    ~zod/try=> (zm:jo `(map term (unit ,@u))`(mo a/`4 b/~ c/`2 ~))
    ~
    ~zod/try=> (~(run by `(map ,@t ,@u)`(mo a/1 b/2 c/3 ~)) (flit |=(a=@ (lth a 5))))
    {[p='a' q=[~ u=1]] [p='c' q=[~ u=3]] [p='b' q=[~ u=2]]}
    ~zod/try=> (zm:jo (~(run by `(map ,@t ,@u)`(mo a/1 b/2 c/3 ~)) (flit |=(a=@ (lth a 5)))))
    [~ {[p='a' q=1] [p='c' q=3] [p='b' q=2]}]
    ~zod/try=> (zm:jo (~(run by `(map ,@t ,@u)`(mo a/1 b/7 c/3 ~)) (flit |=(a=@ (lth a 5)))))
    ~
    ~zod/try=> (~(run by `(map ,@t ,@u)`(mo a/1 b/7 c/3 ~)) (flit |=(a=@ (lth a 5))))
    {[p='a' q=[~ u=1]] [p='c' q=[~ u=3]] [p='b' q=~]}


###++joba

```
++  joba                                                ::  object from k-v pair
  |=  [p=@t q=json]
  ^-  json
  [%o [[p q] ~ ~]]
::
```

JSON object from one key-value

    ~zod/try=> (joba %hi %b |)
    [%o p={[p='hi' q=[%b p=%.n]]}]
    ~zod/try=> (crip (pojo (joba %hi %b |)))
    '{"hi":false}'
    ~zod/try=> (joba %hi (jone 2.130))
    [%o p={[p='hi' q=[%n p=~.2130]]}]
    ~zod/try=> (crip (pojo (joba %hi (jone 2.130))))
    '{"hi":2130}'

###++jobe

```
++  jobe                                                ::  object from k-v list
  |=  a=(list ,[p=@t q=json])
  ^-  json
  [%o (~(gas by *(map ,@t json)) a)]
::
```

JSON object from key-value pairs

    ~zod/try=> (jobe a/n/'20' b/~ c/a/~[s/'mol'] ~)
    [%o p={[p='a' q=[%n p=~.20]] [p='c' q=[%a p=~[[%s p=~.mol]]]] [p='b' q=~]}]
    ~zod/try=> (crip (pojo (jobe a/n/'20' b/~ c/a/~[s/'mol'] ~)))
    '{"b":null,"c":["mol"],"a":20}'
    
###++jape

```
++  jape                                                ::  string from tape
  |=  a=tape
  ^-  json
  [%s (crip a)]
::
```

JSON string from tape

    ~zod/try=> (jape ~)
    [%s p=~.]
    ~zod/try=> (jape "lam")
    [%s p=~.lam]
    ~zod/try=> (crip (pojo (jape "lam")))
    '"lam"'
    ~zod/try=> (crip (pojo (jape "semtek som? zeplo!")))
    '"semtek som? zeplo!"'

###++jone

```
++  jone                                                ::  number from unsigned
  |=  a=@u
  ^-  json
  :-  %n
  ?:  =(0 a)  '0'
  (crip (flop |-(^-(tape ?:(=(0 a) ~ [(add '0' (mod a 10)) $(a (div a 10))])))))
::
```

Unsigned integer as JSON number

    ~zod/try=> (jone 1)
    [%n p=~.1]
    ~zod/try=> (pojo (jone 1))
    "1"
    ~zod/try=> (jone 1.203.196)
    [%n p=~.1203196]
    ~zod/try=> (pojo (jone 1.203.196))
    "1203196"

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

Escape JSON character

    ~zod/try=> (jesc 'a')
    "a"
    ~zod/try=> (jesc 'c')
    "c"
    ~zod/try=> (jesc '\\')
    "\\"
    ~zod/try=> (jesc '"')
    "\""

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
  --
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

An [octs] contains a length, to encode trailing zeroes.

    ~zod/try=> (taco 'abc')
    [p=3 q=6.513.249]
    ~zod/try=> `@t`6.513.249
    'abc'

###++tact

```
++  tact                                                ::  tape to octstream
  |=  tep=tape  ^-  octs
  (taco (rap 3 tep))
::
```

octs from tape

    ~zod/try=> (tact "abc")
    [p=3 q=6.513.249]
    ~zod/try=> `@t`6.513.249
    'abc'

###++tell

```
++  tell                                                ::  wall to octstream
  |=  wol=wall  ^-  octs
  =+  buf=(rap 3 (turn wol |=(a=tape (crip (weld a `tape`[`@`10 ~])))))
  [(met 3 buf) buf]
::
```

octs from wall

    ~zod/try=> (tell ~["abc" "line" "3"])
    [p=11 q=12.330.290.663.108.538.769.039.969]
    ~zod/try=> `@t`12.330.290.663.108.538.769.039.969
    '''
    abc
    line
    3
    '''

###++txml

```
++  txml                                                ::  string to xml
  |=  tep=tape  ^-  manx
  [[%$ [%$ tep] ~] ~]
::
```

Tape to xml CDATA node

    ~zod/try=> (txml "hi")
    [g=[n=%$ a=~[[n=%$ v="hi"]]] c=~]
    ~zod/try=> (txml "larton bestok")
    [g=[n=%$ a=~[[n=%$ v="larton bestok"]]] c=~]
