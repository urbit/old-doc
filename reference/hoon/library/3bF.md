##section 3bF, names etc

###++clan

```
++  clan                                                ::  ship to rank
  |=  who=ship  ^-  rank
  =+  wid=(met 3 who)
  ?:  (lte wid 1)   %czar
  ?:  =(2 wid)      %king
  ?:  (lte wid 4)   %duke
  ?:  (lte wid 8)   %earl
  ?>  (lte wid 16)  %pawn
::
```

XX document

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
```

XX document

###++sifo

```
++  sifo                                                ::  64-bit encode
  |=  tig=@
  ^-  tape
  =+  poc=(mod (sub 3 (mod (met 3 tig) 3)) 3)
  =+  pad=(lsh 3 poc (swap 3 tig))
  =+  ^=  ska
  "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
  =+  ^=  sif
      %-  flop
      |-  ^-  tape
      ?~  pad
        ~
      =+  d=(end 0 6 pad)
      [(snag d ska) $(pad (rsh 0 6 pad))]
  (weld (scag (sub (lent sif) poc) sif) (trip (fil 3 poc '=')))
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
::
```

XX document

###++epur

```
++  epur                                                ::  url/header parser
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
      ?.(=('-' (rsh 3 a (dec (met 3 a)))) [~ u=a] ~)
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
::
```

XX document

###++feel

```
++  feel                                                ::  simple file write
  |=  [pax=path val=*]
  ^-  miso
  =+  dir=((hard arch) .^(%cy pax))
  ?~  q.dir  [%ins val]
  :-  %mut
  ^-  udon
  [%a %a .^(%cx pax) val]
::
```

XX document

###++file

```
++  file                                                ::  simple file load
  |=  pax=path
  ^-  (unit)
  =+  dir=((hard arch) .^(%cy pax))
  ?~(q.dir ~ [~ .^(%cx pax)])
::
```

XX document

###++foal

```
++  foal                                                ::  high-level write
  |=  [pax=path val=*]
  ^-  toro
  ?>  ?=([* * * *] pax)
  [i.t.pax [%& [*cart [[t.t.t.pax (feel pax val)] ~]]]]
::
```

XX document

###++fray

```
++  fray                                                ::  high-level delete
  |=  pax=path
  ^-  toro
  ?>  ?=([* * * *] pax)
  [i.t.pax [%& [*cart [[t.t.t.pax [%del .^(%cx pax)]] ~]]]]
::
```

XX document

###++furl

```
++  furl                                                ::  unify changes
  |=  [one=toro two=toro] 
  ^-  toro
  ~|  %furl
  ?>  ?&  =(p.one p.two)                                ::  same path
          &(?=(& -.q.one) ?=(& -.q.two))                ::  both deltas
      ==
  [p.one [%& [*cart (weld q.q.q.one q.q.q.two)]]]
::
```

XX document

###++glam

```
++  glam
  |=  zar=@p  ^-  tape
  %+  snag  zar
  ^-  (list tape)
  :~  "Tianming"  "Pepin the Short"  "Haile Selassie"  "Alfred the Great"
      "Tamerlane"  "Pericles"  "Talleyrand"  "Yongle"  "Seleucus"
      "Uther Pendragon"  "Louis XVI"  "Ahmad Shāh Durrānī"  "Constantine"
      "Wilhelm I"  "Akbar"  "Louis XIV"  "Nobunaga"  "Alexander VI"
      "Philippe II"  "Julius II"  "David"  "Niall Noígíallach"  "Kublai Khan"
      "Öz Beg Khan"  "Ozymandias"  "Ögedei Khan"  "Jiang Jieshi"  "Darius"
      "Shivaji"  "Qianlong"  "Bolesław I Chrobry"  "Tigranes"  "Han Wudi"
      "Charles X"  "Naresuan"  "Frederick II"  "Simeon"  "Kangxi"
      "Suleiman the Magnificent"  "Pedro II"  "Genghis Khan"  "Laozi"
      "Porfirio Díaz"  "Pakal"  "Wu Zetian"  "Garibaldi"  "Matthias Corvinus"
      "Leopold II"  "Leonidas"  "Sitting Bull"  "Nebuchadnezzar II"
      "Rhodes"  "Henry VIII"  "Attila"  "Catherine II"  "Chulalongkorn"
      "Uthmān"  "Augustus"  "Faustin"  "Chongde"  "Justinian"
      "Afonso de Albuquerque"  "Antoninus Pius"  "Cromwell"  "Innocent X"
      "Fidel"  "Frederick the Great"  "Canute"  "Vytautas"  "Amina"
      "Hammurabi"  "Suharto"  "Victoria"  "Hiawatha"  "Paul V"  "Shaka"
      "Lê Thánh Tông"  "Ivan Asen II"  "Tiridates"  "Nefertiti"  "Gwangmu"
      "Ferdinand & Isabella"  "Askia"  "Xuande"  "Boris Godunov"  "Gilgamesh"
      "Maximillian I"  "Mao"  "Charlemagne"  "Narai"  "Hanno"  "Charles I & V"
      "Alexander II"  "Mansa Musa"  "Zoe Porphyrogenita"  "Metternich"
      "Robert the Bruce"  "Pachacutec"  "Jefferson"  "Solomon"  "Nicholas I"
      "Barbarossa"  "FDR"  "Pius X"  "Gwanggaeto"  "Abbas I"  "Julius Caesar"
      "Lee Kuan Yew"  "Ranavalona I"  "Go-Daigo"  "Zenobia"  "Henry V"
      "Bảo Đại"  "Casimir III"  "Cyrus"  "Charles the Wise"  "Sandrokottos"
      "Agamemnon"  "Clement VII"  "Suppiluliuma"  "Deng Xiaoping"
      "Victor Emmanuel"  "Ajatasatru"  "Jan Sobieski"  "Huangdi"  "Xuantong"
      "Narmer"  "Cosimo de' Medici"  "Möngke Khan"  "Stephen Dušan"  "Henri IV"
      "Mehmed Fatih"  "Conn Cétchathach"  "Francisco Franco"  "Leo X"
      "Kammu"  "Krishnadevaraya"  "Elizabeth I"  "Norton I"  "Washington"
      "Meiji"  "Umar"  "TR"  "Peter the Great"  "Agustin I"  "Ashoka"
      "William the Conqueror"  "Kongolo Mwamba"  "Song Taizu"
      "Ivan the Terrible"  "Yao"  "Vercingetorix"  "Geronimo"  "Rurik"
      "Urban VIII"  "Alexios Komnenos"  "Maria I"  "Tamar"  "Bismarck"
      "Arthur"  "Jimmu"  "Gustavus Adolphus"  "Suiko"  "Basil I"  "Montezuma"
      "Santa Anna"  "Xerxes"  "Beyazıt Yıldırım"  "Samudragupta"  "James I"
      "George III"  "Kamehameha"  "Francesco Sforza"  "Trajan"
      "Rajendra Chola"  "Hideyoshi"  "Cleopatra"  "Alexander"
      "Ashurbanipal"  "Paul III"  "Vespasian"  "Tecumseh"  "Narasimhavarman"
      "Suryavarman II"  "Bokassa I"  "Charles Canning"  "Theodosius"
      "Francis II"  "Zhou Wen"  "William Jardine"  "Ahmad al-Mansur"
      "Lajos Nagy"  "Theodora"  "Mussolini"  "Samuil"  "Osman Gazi"
      "Kim Il-sung"  "Maria Theresa"  "Lenin"  "Tokugawa"  "Marcus Aurelius"
      "Nzinga Mbande"  "Edward III"  "Joseph II"  "Pulakesi II"  "Priam"
      "Qin Shi Huang"  "Shah Jahan"  "Sejong"  "Sui Wendi"  "Otto I"
      "Napoleon III"  "Prester John"  "Dido"  "Joao I"  "Gregory I"
      "Gajah Mada"  "Abd-ar Rahmān III"  "Taizong"  "Franz Josef I"
      "Nicholas II"  "Gandhi"  "Chandragupta II"  "Peter III"
      "Oba Ewuare"  "Louis IX"  "Napoleon"  "Selim Yavuz"  "Shun"
      "Hayam Wuruk"  "Jagiełło"  "Nicaule"  "Sargon"  "Saladin"  "Charles II"
      "Brian Boru"  "Da Yu"  "Antiochus III"  "Charles I"
      "Jan Pieterszoon Coen"  "Hongwu"  "Mithridates"  "Hadrian"  "Ptolemy"
      "Benito Juarez"  "Sun Yat-sen"  "Raja Raja Chola"  "Bolivar"  "Pius VII"
      "Shapur II"  "Taksin"  "Ram Khamhaeng"  "Hatshepsut"  "Alī"  "Matilda"
      "Ataturk"
  ==
::
```

XX document

###++glon

```
++  glon
  |=  lag=lang
  ^-  (unit tape)
  ?+  lag  ~
    %aa  [~ "Afar"]
    %ab  [~ "Abkhazian"]
    %ae  [~ "Avestan"]
    %af  [~ "Afrikaans"]
    %ak  [~ "Akan"]
    %am  [~ "Amharic"]
    %an  [~ "Aragonese"]
    %ar  [~ "Arabic"]
    %as  [~ "Assamese"]
    %av  [~ "Avaric"]
    %ay  [~ "Aymara"]
    %az  [~ "Azerbaijani"]
    %ba  [~ "Bashkir"]
    %be  [~ "Belarusian"]
    %bg  [~ "Bulgarian"]
    %bh  [~ "Bihari"]
    %bi  [~ "Bislama"]
    %bm  [~ "Bambara"]
    %bn  [~ "Bengali"]
    %bo  [~ "Tibetan"]
    %br  [~ "Breton"]
    %bs  [~ "Bosnian"]
    %ca  [~ "Catalan"]
    %ce  [~ "Chechen"]
    %ch  [~ "Chamorro"]
    %co  [~ "Corsican"]
    %cr  [~ "Cree"]
    %cs  [~ "Czech"]
    %cu  [~ "Slavonic"]
    %cv  [~ "Chuvash"]
    %cy  [~ "Welsh"]
    %da  [~ "Danish"]
    %de  [~ "German"]
    %dv  [~ "Maldivian"]
    %dz  [~ "Dzongkha"]
    %ee  [~ "Ewe"]
    %el  [~ "Greek"]
    %en  [~ "English"]
    %eo  [~ "Esperanto"]
    %es  [~ "Spanish"]
    %et  [~ "Estonian"]
    %eu  [~ "Basque"]
    %fa  [~ "Persian"]
    %ff  [~ "Fulah"]
    %fi  [~ "Finnish"]
    %fj  [~ "Fijian"]
    %fo  [~ "Faroese"]
    %fr  [~ "French"]
    %fy  [~ "Frisian"]
    %ga  [~ "Irish Gaelic"]
    %gd  [~ "Scottish Gaelic"]
    %gl  [~ "Galician"]
    %gn  [~ "Guarani"]
    %gu  [~ "Gujarati"]
    %gv  [~ "Manx"]
    %ha  [~ "Hausa"]
    %he  [~ "Hebrew"]
    %hi  [~ "Hindi"]
    %ho  [~ "Hiri Motu"]
    %hr  [~ "Croatian"]
    %ht  [~ "Haitian Creole"]
    %hu  [~ "Hungarian"]
    %hy  [~ "Armenian"]
    %hz  [~ "Herero"]
    %ia  [~ "Interlingua"]
    %id  [~ "Indonesian"]
    %ie  [~ "Occidental"]
    %ig  [~ "Igbo"]
    %ii  [~ "Nuosu"]
    %ik  [~ "Inupiaq"]
    %io  [~ "Ido"]
    %is  [~ "Icelandic"]
    %it  [~ "Italian"]
    %iu  [~ "Inuktitut"]
    %ja  [~ "Japanese"]
    %jv  [~ "Javanese"]
    %ka  [~ "Georgian"]
    %kg  [~ "Kongo"]
    %ki  [~ "Kikuyu"]
    %kj  [~ "Kwanyama"]
    %kk  [~ "Kazakh"]
    %kl  [~ "Kalaallisut"]
    %km  [~ "Central Khmer"]
    %kn  [~ "Kannada"]
    %ko  [~ "Korean"]
    %kr  [~ "Kanuri"]
    %ks  [~ "Kashmiri"]
    %ku  [~ "Kurdish"]
    %kv  [~ "Komi"]
    %kw  [~ "Cornish"]
    %ky  [~ "Kyrgyz"]
    %la  [~ "Latin"]
    %lb  [~ "Luxembourgish"]
    %lg  [~ "Ganda"]
    %li  [~ "Limburgish"]
    %ln  [~ "Lingala"]
    %lo  [~ "Lao"]
    %lt  [~ "Lithuanian"]
    %lu  [~ "Luba-Katanga"]
    %lv  [~ "Latvian"]
    %mg  [~ "Malagasy"]
    %mh  [~ "Marshallese"]
    %mi  [~ "Maori"]
    %mk  [~ "Macedonian"]
    %ml  [~ "Malayalam"]
    %mn  [~ "Mongolian"]
    %mr  [~ "Marathi"]
    %ms  [~ "Malay"]
    %mt  [~ "Maltese"]
    %my  [~ "Burmese"]
    %na  [~ "Nauru"]
    %nb  [~ "Norwegian Bokmål"]
    %nd  [~ "North Ndebele"]
    %ne  [~ "Nepali"]
    %ng  [~ "Ndonga"]
    %nl  [~ "Dutch"]
    %nn  [~ "Norwegian Nynorsk"]
    %no  [~ "Norwegian"]
    %nr  [~ "South Ndebele"]
    %nv  [~ "Navajo"]
    %ny  [~ "Chichewa"]
    %oc  [~ "Occitan"]
    %oj  [~ "Ojibwa"]
    %om  [~ "Oromo"]
    %or  [~ "Oriya"]
    %os  [~ "Ossetian"]
    %pa  [~ "Punjabi"]
    %pi  [~ "Pali"]
    %pl  [~ "Polish"]
    %ps  [~ "Pashto"]
    %pt  [~ "Portuguese"]
    %qu  [~ "Quechua"]
    %rm  [~ "Romansh"]
    %rn  [~ "Rundi"]
    %ro  [~ "Romanian"]
    %ru  [~ "Russian"]
    %rw  [~ "Kinyarwanda"]
    %sa  [~ "Sanskrit"]
    %sc  [~ "Sardinian"]
    %sd  [~ "Sindhi"]
    %se  [~ "Northern Sami"]
    %sg  [~ "Sango"]
    %si  [~ "Sinhala"]
    %sk  [~ "Slovak"]
    %sl  [~ "Slovenian"]
    %sm  [~ "Samoan"]
    %sn  [~ "Shona"]
    %so  [~ "Somali"]
    %sq  [~ "Albanian"]
    %sr  [~ "Serbian"]
    %ss  [~ "Swati"]
    %st  [~ "Sotho"]
    %su  [~ "Sundanese"]
    %sv  [~ "Swedish"]
    %sw  [~ "Swahili"]
    %ta  [~ "Tamil"]
    %te  [~ "Telugu"]
    %tg  [~ "Tajik"]
    %th  [~ "Thai"]
    %ti  [~ "Tigrinya"]
    %tk  [~ "Turkmen"]
    %tl  [~ "Tagalog"]
    %tn  [~ "Tswana"]
    %to  [~ "Tonga"]
    %tr  [~ "Turkish"]
    %ts  [~ "Tsonga"]
    %tt  [~ "Tatar"]
    %tw  [~ "Twi"]
    %ty  [~ "Tahitian"]
    %ug  [~ "Uighur"]
    %uk  [~ "Ukrainian"]
    %ur  [~ "Urdu"]
    %uz  [~ "Uzbek"]
    %ve  [~ "Venda"]
    %vi  [~ "Vietnamese"]
    %vo  [~ "Volapük"]
    %wa  [~ "Walloon"]
    %wo  [~ "Wolof"]
    %xh  [~ "Xhosa"]
    %yi  [~ "Yiddish"]
    %yo  [~ "Yoruba"]
    %za  [~ "Zhuang"]
    %zh  [~ "Chinese"]
    %zu  [~ "Zulu"]
  ==
::
```

XX document

###++gnow

```
++  gnow
  |=  [who=@p gos=gcos]  ^-  @t
  ?-    -.gos
      %czar                 (rap 3 '|' (rap 3 (glam who)) '|' ~)
      %king                 (rap 3 '_' p.gos '_' ~)
      %earl                 (rap 3 ':' p.gos ':' ~)
      %pawn                 ?~(p.gos %$ (rap 3 '.' u.p.gos '.' ~))
      %duke
    ?:  ?=(%anon -.p.gos)  %$
    %+  rap  3
    ^-  (list ,@)
    ?-    -.p.gos
        %punk  ~['"' q.p.gos '"']
        ?(%lord %lady)
      =+  ^=  nad
          =+  nam=`name`s.p.p.gos
          %+  rap  3
          :~  p.nam
              ?~(q.nam 0 (cat 3 ' ' u.q.nam))
              ?~(r.nam 0 (rap 3 ' (' u.r.nam ')' ~))
              ' '
              s.nam
          ==
      ?:(=(%lord -.p.gos) ~['[' nad ']'] ~['(' nad ')'])
    ==
  ==
::
```

XX document

###++hunt

```
++  hunt                                                ::  first of unit dates
  |=  [one=(unit ,@da) two=(unit ,@da)]
  ^-  (unit ,@da)
  ?~  one  two
  ?~  two  one
  ?:((lth u.one u.two) one two)
::
```

XX document

###++meat

```
++  meat                                                ::  kite to .^ path
  |=  kit=kite
  ^-  path
  [(cat 3 'c' p.kit) (scot %p r.kit) s.kit (scot (dime q.kit)) t.kit]
::
```

XX document

###++mojo

```
++  mojo                                                ::  compiling load
  |=  [pax=path src=*]
  ^-  (each twig (list tank))
  ?.  ?=(@ src)
    [%| ~[[leaf/"musk: malformed: {<pax>}"]]]
  =+  ^=  mud
      %-  mule  |.
      ((full vest) [1 1] (trip src))
  ?:  ?=(| -.mud)  mud
  ?~  q.p.mud
    :~  %|
        leaf/"musk: syntax error: {<pax>}"
        leaf/"musk: line {<p.p.p.mud>}, column {<q.p.p.mud>}"
    ==
  [%& p.u.q.p.mud]
::
```

XX document

###++mole

```
++  mole                                                ::  new to old sky
  |=  ska=$+(* (unit (unit)))
  |=  a=*
  ^-  (unit)
  =+  b=(ska a)
  ?~  b  ~
  ?~  u.b  ~
  [~ u.u.b]
::
```

XX document

###++much

```
++  much                                                ::  constructing load
  |=  [pax=path src=*]
  ^-  gank
   =+  moj=(mojo pax src)
  ?:  ?=(| -.moj)  moj
  (mule |.((slap !>(+>.$) `twig`p.moj)))
::
```

XX document

###++musk

```
++  musk                                                ::  compiling apply
  |=  [pax=path src=* sam=vase]
  ^-  gank
  =+  mud=(much pax src)
  ?:  ?=(| -.mud)  mud
  (mule |.((slam p.mud sam)))
::
```

XX document

###++numb

```
++  numb                                                ::  ship display name
  |=  [him=@p our=@p now=@da]  ^-  @t
  =+  yow=(scot %p him)
  =+  pax=[(scot %p our) %name (scot %da now) yow ~]
  =+  woy=((hard ,@t) .^(%a pax))
  ?:  =(%$ woy)  yow
  (cat 3 yow (cat 3 ' ' woy))
::
```

XX document

###++saxo

```
++  saxo                                                ::  autocanon
  |=  who=ship
  ^-  (list ship)
  ?:  (lth who 256)  [who ~]
  [who $(who (sein who))]
::
```

XX document

###++sein

```
++  sein                                                ::  autoboss
  |=  who=ship  ^-  ship
  =+  mir=(clan who)
  ?-  mir
    %czar  who
    %king  (end 3 1 who)
    %duke  (end 4 1 who)
    %earl  (end 5 1 who)
    %pawn  `@p`0
  ==
::
```

XX document

###++tame

```
++  tame
  |=  hap=path
  ^-  (unit kite)
  ?.  ?=([@ @ @ @ *] hap)  ~
  =+  :*  hyr=(slay i.hap)
          fal=(slay i.t.hap)
          dyc=(slay i.t.t.hap)
          ved=(slay i.t.t.t.hap)
          ::  ved=(slay i.t.hap)
          ::  fal=(slay i.t.t.hap)
          ::  dyc=(slay i.t.t.t.hap)
          tyl=t.t.t.t.hap
      ==
  ?.  ?=([~ %$ %tas @] hyr)  ~
  ?.  ?=([~ %$ %p @] fal)  ~
  ?.  ?=([~ %$ %tas @] dyc)  ~
  ?.  ?=(^ ved)  ~
  =+  his=`@p`q.p.u.fal
  =+  [dis=(end 3 1 q.p.u.hyr) rem=(rsh 3 1 q.p.u.hyr)]
  ?.  ?&(?=(%c dis) ?=(?(%v %w %x %y %z) rem))  ~
  [~ rem (case p.u.ved) q.p.u.fal q.p.u.dyc tyl]
::
```

XX document

###++tome

```
++  tome                                                ::  parse path
  |=  pax=path
  ^-  (unit beam)
  ?.  ?=([* * * *] pax)  ~
  %+  biff  (slaw %p i.pax)
  |=  who=ship
  %+  biff  (slaw %tas i.t.pax)
  |=  dex=desk
  %+  biff  (slay i.t.t.pax)
  |=  cis=coin
  ?.  ?=([%$ case] cis)  ~
  `(unit beam)`[~ [who dex `case`p.cis] (flop t.t.t.pax)]
::
```

XX document

###++tope

```
++  tope                                                ::  beam to path
  |=  bem=beam
  ^-  path
  [(scot %p p.bem) q.bem (scot r.bem) (flop s.bem)]
```

XX document

