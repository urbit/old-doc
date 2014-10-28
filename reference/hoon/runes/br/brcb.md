#[barcab, `|_`, %brcb](#brcb)

Door with sample

`|_` is a synthetic hoon that produces a [`%gold`]() [door]() with sample `p`, arms `q`. `|_` takes an associative list of names, [++term](), and expressions [++foot](), each pair of which is called an arm. The list must be closed with a `--`. `|_` is similar to `|%`, but defines a sample for the set of arms it contains. 
##Produces

Twig: `[%brcb p=tile q=(map term foot)]`

##Sample

`p` is a [tile]().
`q` is a [`map`]() with [`++term`]() keys and [`++foot`]() values.

##Tall form

    |_  p
        ++  p.n.q
          q.n.q
        --

##Wide form

None

##Irregular form

None

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

In this example we create a door `mol` that operates on a [`@ud`](), `a`. We add two arms to our door, `++succ` and `++prev` and test invoking them with the irregular form of `%~`. Doors are commonly invoked with `%~`, irregular form `~(arm door sample)`, which replaces the door's sample and pulls the specified arm.

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

`++ne` is used to print a single digit in base 10, 16, 32, or 64 and is a part of the hoon standard library. You can find it in `hoon.hoon`. `|_` is very commonly used throughout our standard library for groups of arms who all take the same sample. 

    ~zod/try=> ~(x ne 12)
    99
    ~zod/try=> `@t`~(x ne 12)
    'c'
    ~zod/try=> `@ux`12
    0xc

Here we put `++ne` to work a bit. Our first call renders 12 in base 16. Since `99` is within the ASCII character range, we can cast it to a [`@t`]() and get `'c'`. Conveniently, casting `12` to a [`@ux`]() results in `0xc`.
