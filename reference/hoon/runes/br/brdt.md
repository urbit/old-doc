#[bardot, `|.`, %brdt](#brdt)

Trap

`|.`, is a synthetic hoon that produces a dry [`%gold`]() trap. You can think of it like a 'trap door', since `|.` is a [`door`]() with one arm [`$`](), the empty name. The default action performed on a trap is kicking it by pulling the arm `$`. `|.` is similar to `|=` with no arguments.

##Produces

Twig: `[%brdt p=twig]`

##Sample

`p` is a [`++twig`]().

##Tall form

    |.  p

##Wide form

    |.(p)

##Irregular form

None

##Examples

    /~zod/try=> 
    =a  |.(42)
    changed %a
    /~zod/try=> 
    a
    < 1.yln
      [   a
        < 2.yqy
          [   a
            < 3.kii
              [   a
                < 2.wvx
                  [ a=<2.kqf 2.hng 250.qyy 41.raw 414.hhh 100.xkc 1.ypj %164>
                    <2.hng 250.qyy 41.raw 414.hhh 100.xkc 1.ypj %164>
                  ]
                >
                <2.hng 250.qyy 41.raw 414.hhh 100.xkc 1.ypj %164>
              ]
            >
            <2.hng 250.qyy 41.raw 414.hhh 100.xkc 1.ypj %164>
          ]
        >
        <2.hng 250.qyy 41.raw 414.hhh 100.xkc 1.ypj %164>
      ]
    >
    /~zod/try=> 
    (a)
    42
    /~zod/try=> 
    $:a
    42

This is a simple example. We assign a shell variable `a` to be a trap that just produces the atom `42`. Printing `a` prints the core and its context. Calling `a` using `(`, the irregular form of [`%-`](), produces its value. As does pulling the arm `$` from inside it using `$:a`.

    /~zod/try=> 
    =a  10
    changed %a
    /~zod/try=> 
    =b  |.  (add a 2)
    changed %b
    /~zod/try=> 
    (b)
    12

In this case we assign a variable `a` to be `10`, and create a trap `b` to add `2` to it. This is a trivial example, but is meant to show that traps are useful when you need a gate that only operates on values that are already in its context. 
