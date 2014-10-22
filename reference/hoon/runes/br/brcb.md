#[barcab, `|_`, %brcb](#brcb)

[Short description]

#Syntax

`|_`, `barcab`, `[%brcb p=tile q=(map term foot)]` is a synthetic hoon that
produces a `%gold` door with sample `p`, arms `q`. `|_` takes an associative
array of names (++term) and expressions (++foot), each pair of which is called
an arm. A dry, or %ash, arm is denoted with `++`. `|_` can take an arbitrary
number of arms, but the arm array must be terminated with a `--`

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|_  p
    ++  p.n.q
      q.n.q
    --

##Wide form

None

##Irregular form

None

##Reduction

[`=|`]()  [`|%` ]()
See also: [%brcb:++open:al]()

##Examples

    /~zod/try=> =mol
                  |_  a=@ud
                  ++  succ  +(a)
                  ++  prev  (dec a)
                  --
    /~zod/try=> ~(succ mol 1)
    2
    /~zod/try=> ~(succ mol ~(succ mol ~(prev mol 5)))
    6

Here we create a door `mol` that operates on a `@ud`, `a`. We add two arms to our door, `++succ` and `++prev` and test invoking them with the irregular form of `%~`. Doors are commonly invoked with `%~`, irregular form `~(arm door sample)`, which replaces the door's sample and pulls the specified arm.

```
++  ne
  |_  tig=@
  ++  d  (add tig '0')
  ++  x  ?:((gte tig 10) (add tig 87) d)
  ++  v  ?:((gte tig 10) (add tig 87) d)
  ++  w  ?:(=(tig 63) '~' ?:(=(tig 62) '-' ?:((gte tig 36) (add tig 29) x)))
  --
::
```

++ne is used to print a single digit in base 10, 16, 32, or 64

    ~zod/try=> `@t`~(x ne 12)
    'c'
    ~zod/try=> `@ux`12
    0xc
