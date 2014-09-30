section 2eO, virtualization
---

###++mack

```
++  mack
  |=  [sub=* fol=*]
  ^-  (unit)
  =+  ton=(mink [sub fol] |=(* ~))
  ?.(?=([0 *] ton) ~ [~ p.ton])
::
```

Accpet a nock subject-formula cell.
Produce a unit result, treating 11 as a crash (i.e. pure nock).

####Summary

        Creates a dry %gold gate accepting cell ['sub' 'fol'].
        Its output is a unit (of a noun).
        Let 'ton' be the result of minking the sample, with a sky that produces
        ~ on any input, halting interpretation.
        Unless ton has stem 0, produce the empty unit, otherwise produce one
        containing ton's bulb.

####Examples

        ~zod/try=> (mack [[1 2 3] [0 1]])
        [~ [1 2 3]]
        ~zod/try=> (mack [41 4 0 1])
        [~ 42]
        ~zod/try=> (mack [4 0 4])
        ~
        ~zod/try=> (mack [[[0 2] [1 3]] 4 4 4 4 0 5])
        [~ 6]
        ~zod/try=> ;;((unit ,@tas) (mack [[1 %yes %no] 6 [0 2] [0 6] 0 7]))
        [~ %no]

###++mink

```
++  mink
  ~/  %mink
  |=  [[sub=* fol=*] sky=$+(* (unit))]
  =+  tax=*(list ,[@ta *])
  |-  ^-  tone
  ?@  fol
    [%2 tax]
  ?:  ?=(^ -.fol)
    =+  hed=$(fol -.fol)
    ?:  ?=(%2 -.hed)
      hed
    =+  tal=$(fol +.fol)
    ?-  -.tal
      %0  ?-(-.hed %0 [%0 p.hed p.tal], %1 hed)
      %1  ?-(-.hed %0 tal, %1 [%1 (weld p.hed p.tal)])
      %2  tal
    ==
  ?+    fol
    [%2 tax]
  ::
      [0 b=@]
    ?:  =(0 b.fol)  [%2 tax]
    ?:  =(1 b.fol)  [%0 sub]
    ?:  ?=(@ sub)   [%2 tax]
    =+  [now=(cap b.fol) lat=(mas b.fol)]
    $(b.fol lat, sub ?:(=(2 now) -.sub +.sub))
  ::
      [1 b=*]
    [%0 b.fol]
  ::
      [2 b=[^ *]]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    ?>(?=(^ p.ben) $(sub -.p.ben, fol +.p.ben))
    ::?>(?=(^ p.ben) $([sub fol] p.ben)
  ::
      [3 b=*]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    [%0 .?(p.ben)]
  ::
      [4 b=*]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    ?.  ?=(@ p.ben)  [%2 tax]
    [%0 .+(p.ben)]
  ::
      [5 b=*]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    ?.  ?=(^ p.ben)  [%2 tax]
    [%0 =(-.p.ben +.p.ben)]
  ::
      [6 b=* c=* d=*]
    $(fol =>(fol [2 [0 1] 2 [1 c d] [1 0] 2 [1 2 3] [1 0] 4 4 b]))
  ::
      [7 b=* c=*]       $(fol =>(fol [2 b 1 c]))
      [8 b=* c=*]       $(fol =>(fol [7 [[0 1] b] c]))
      [9 b=* c=*]       $(fol =>(fol [7 c 0 b]))
      [10 @ c=*]        $(fol c.fol)
      [10 [b=* c=*] d=*]
    =+  ben=$(fol c.fol)
    ?.  ?=(%0 -.ben)  ben
    ?:  ?=(?(%hunk %lose %mean %spot) b.fol)
      $(fol d.fol, tax [[b.fol p.ben] tax])
    $(fol d.fol)
  ::
      [11 b=*]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    =+  val=(sky p.ben)
    ?~(val [%1 p.ben ~] [%0 u.val])
  ::
  ==
::
```

Bottom-level mock (virtual nock) interpreter.

####Summary

        Accepts a nock subject-formula cell, and an %iron gate which 
          accepts any noun and produces a unit, which is defined to be mock 11.
        Produces a ++tone, which is the result of the virtualized computation.
        ---
        For clarity, a ++tone with stem %0 will be referred to as a "success",
        one with stem %1 as a "block", and one with stem %2 as a "crash".
        ---
        Activate jet.
        Creates a dry %gold gate accepting cell ['sub' 'fol'] and gate 'sky'.
        Let 'tax' be a statically bunted list of term-noun pairs. (hint list)
        Do (recursion point) produce a tone:
        If fol is an atom
          Produce a crash of fol.
        Else if the head of fol is a cell
          Let hed be the result of recurring with fol replaced by its head.
          If hed is a crash
            Yield it
          Otherwise let 'tal' be the result of recurring with fol replaced 
          by its tail.
          Switch on the type of tal by stem:
            If tal is a success
              If hed is a block produce hed.
              Else (success) produce a success of a cell of the bulbs of hed 
              and tal.
            If tal is a block
              If hed is a success produce tal.
              Else (block) produce a block of welding the bulbs of hed and tal.
            Else (crash) produce tal
        Otherwise (the head of fol is an atom) switch on fol,
          by default producing a crash of tax.
            If fol has stem 0 and an atom bulb we name 'b'
          If b is 0 produce a crash of tax.
          If b is 1 produce a success of sub.
          If sub is an atom produce a crash of tax
          Otherwise let 'now' be the cap of b, and 'lat' be the mas of b
          Tail-recur with b replaced by lat, and sub replaced by: if now is 2,
          its head, else its tail.
            If fol has stem 1 and a bulb we name 'b'
          Produce a success of b
            If fol has stem 2 and a bulb whose head is a cell.
          Let 'ben' be the result of recurring with fol replaced by its bulb.
          Unless ben is a success, produce ben.
          Else assert that ben contains a cell, and tail-recur with 
          sub and fol replaced by the head and tail of ben's bulb
            If fol has stem 3 and a bulb we name 'b'
          Let 'ben' be the result of recurring with fol replaced by b.
          Unless ben is a success, produce ben.
          Else produce a success of (loobean) whether ben contains a cell.
            If fol has stem 4 and a bulb we name 'b'
          Let 'ben' be the result of recurring with fol replaced by b.
          Unless ben is a success, produce ben.
          Else unless ben contains an atom produce a crash of tax.
          Otherwise produce a success of ben's contents, incremented.
            If fol has stem 5 and a bulb we name 'b'
          Let 'ben' be the result of recurring with fol replaced by b.
          Unless ben is a success, produce ben.
          Else unless ben contains a cell produce a crash of tax.
          Otherwise produce a success of (loobean) whether the bulb of ben has
          a tail equal to its head.
            If fol has stem 6, 7, 8, or 9
          Tail-recur with its bulb expanded per nock specification.
            If fol has stem 10 and a cell bulb whose head is an atom
          Tail-recur with for replaced by its bulb's tail
            If fol has stem 10 and a bulb that can be destructured as [[b c] d]
          Let ben be the result of recurring with fol replaced by v.
          Unless ben is a success, produce ben.
          If b is %hunk, %lose, %mean, or %spot
            Tail-recur with fol replaced by d and tax prepended with a pair of
            b and the bulb of ben.
          Else tail-recur with just fol replaced by d.

####Examples

        XX

###++mock

```
++  mock
  |=  [[sub=* fol=*] sky=$+(* (unit))]
  (mook (mink [sub fol] sky))
::
```

Accepts a nock subject-formula cell and an %iron gate which
accepts any noun and produces a unit (this is used as nock 11).
Produces a ++toon, which is a sucesful, blocked, or crashed result.

####Summary

        Compose ++mook and ++mink.

####Examples 

        ~zod/try=> (mock [5 4 0 1] ,~)
        [%0 p=6]
        ~zod/try=> (mock [~ 11 1 0] |=(* `999))
        [%0 p=999]
        ~zod/try=> (mock [~ 0 1.337] ,~)
        [%2 p=~]
        ~zod/try=> (mock [~ 11 1 1.337] ,~)
        [%1 p=~[1.337]]
        ~zod/try=> (mock [[[4 4 4 4 0 3] 10] 11 9 2 0 1] |=(* `[+<]))
        [%0 p=14]
        ~zod/try=> (mock [[[4 4 4 4 0 3] 10] 11 9 2 0 1] |=(* `[<+<>]))
        [%0 p=[49 52 0]]
        ~zod/try=> ;;(tape +:(mock [[[4 4 4 4 0 3] 10] 11 9 2 0 1] |=(* `[<+<>])))
        "14"

###++mook

```
++  mook
  |=  ton=tone
  ^-  toon
  ?.  ?=([2 *] ton)  ton
  :-  %2
  =+  yel=(lent p.ton)
  =.  p.ton
    ?.  (gth yel 256)  p.ton
    %+  weld
      (scag 128 p.ton)
    ^-  (list ,[@ta *])
    :_  (slag (sub yel 128) p.ton)
    :-  %lose
    %+  rap  3
    ;:  weld
      "[skipped "
      ~(rend co %$ %ud (sub yel 256))
      " frames]"
    ==
  |-  ^-  (list tank)
  ?~  p.ton  ~
  =+  rex=$(p.ton t.p.ton)
  ?+    -.i.p.ton  rex
      %hunk  [(tank +.i.p.ton) rex]
      %lose  [[%leaf (rip 3 (,@ +.i.p.ton))] rex]
      %mean  :_  rex
             ?@  +.i.p.ton  [%leaf (rip 3 (,@ +.i.p.ton))]
             =+  mac=(mack +.i.p.ton +<.i.p.ton)
             ?~(mac [%leaf "####"] (tank u.mac))
      %spot  :_  rex
             =+  sot=(spot +.i.p.ton)
             :-  %leaf
             ;:  weld
               ~(ram re (smyt p.sot))
               ":<["
               ~(rend co ~ %ud p.p.q.sot)
               " "
               ~(rend co ~ %ud q.p.q.sot)
               "].["
               ~(rend co ~ %ud p.q.q.sot)
               " "
               ~(rend co ~ %ud q.q.q.sot)
               "]>"
             ==
  ==
::
```

Intelligently render crash annotation.

####Summary

        Accepts a ++tone, produces a ++toon
        ---
        Create a dry %gold gate accepting a tone we name 'ton'
        Its output is a toon.
        Unless the stem of ton is %2, produce ton.
        Produce a frond with a stem of 2 and the following bulb:
        Let yel be the length of ton's bulb.
        Replace the bulb of ton,
          If yel > 256 (otherwise keep it static)
          With the weld of
            its top 128 elements
          And a list of term-noun pairs:
          The last 128 elements of ton's bulb
          Preceded by a %lose-stemmed frond of
          A cord from the tape
            "[skipped "
            A @ud rendering of yel - 256
            " frames]"
        Do (*recursion point*) produce a list of tanks:
        For each element in the bulb of ton
        Switch on its leaf, by default leaving the element out of the product
          For each %hunk, clam it to a tank
          For each %lose, produce a leaf with the element clammed to an atom 
          and tripped (to a tape).
          For each %mean, if the elment is an atom treat it as a %lose
              Otherwise let mac be the element macked by its tail.
              If the computation fails, produce a "####" leaf, else clam
              the result to a tank.
          For each %spot, let sot be the element clammed to a spot.
              Produce a leaf with
              The weld of
                The path in sot converted to a tank and then a tape
                ":<["
                [[p.p ] ] in the pint in sot rendered as @ud
                " "
                [[ q.p] ] in the pint in sot rendered as @ud
                "].["
                [ [p.q ]] in the pint in sot rendered as @ud
                " "
                [ [ q.p]] in the pint in sot rendered as @ud
                "]>"
                
####Examples 

        ~zod/try=> (mook [%0 5 4 5 1])
        [%0 p=[5 4 5 1]]
        ~zod/try=> (mook [%2 ~[[%hunk %rose ["<" "," ">"] ~[[%leaf "err"]]]]])
        [%2 p=~[[%rose p=[p="<" q="," r=">"] q=[i=[%leaf p="err"] t=~]]]]
        ~zod/try=> (mook [%2 ~[[%malformed %elem] [%lose 'do print']]])
        [%2 p=~[[%leaf p="do print"]]]
        ~zod/try=> (mook [%2 ~[[%spot /b/repl [[1 1] 1 2]] [%mean |.(!!)]]])
        [%2 p=~[[%leaf p="/b/repl/:<[1 1].[1 2]>"] [%leaf p="####"]]]

---

###++mang

```
++  mang
  |=  [[gat=* sam=*] sky=$+(* (unit))]
  ^-  (unit)
  =+  ton=(mong [[gat sam] sky])
  ?.(?=([0 *] ton) ~ [~ p.ton])
::
```

Work just like in `++makc`, but accept a `++sky`.
Produce a unit computation result.

####Summary

        Creates a dry %gold gate accepting cell ['sub' 'fol'] and an
        %iron unit-clam 'sky'.
        Its output is a unit (of a noun).
        Let 'ton' be the result of monging the sample.
        Unless ton has stem 0, produce the empty unit, otherwise produce one
        containing ton's bulb.
---

###++mung

```
++  mung
  |=  [[gat=* sam=*] sky=$+(* (unit))]
  ^-  tone
  ?.  &(?=(^ gat) ?=(^ +.gat))
    [%2 ~]
  (mink [[-.gat [sam +>.gat]] -.gat] sky)
::
```

---

###++mule 

```
++  mule                                                ::  typed virtual
  ~/  %mule
  |*  taq=_|.(_*)
  =+  mud=(mute taq)
  ?-  -.mud
    &  [%& p=$:taq]
    |  [%| p=p.mud]
  ==
::
```

---

###++mute 

```
++  mute                                                ::  untyped virtual
  |=  taq=_^?(|.(_*))
  ^-  (each ,* (list tank))
  =+  ton=(mock [taq 9 2 0 1] |=(* ~))
  ?-  -.ton
    %0  [%& p.ton]
    %1  [%| (turn p.ton |=(a=* (smyt (path a))))]
    %2  [%| p.ton]
  ==
```

---

