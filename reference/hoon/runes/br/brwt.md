#[barwut, `|?`, %brwt](#brwt)

[Short description]

#Syntax

`|?`, `barwut`, `[%brwt q=twig]` is a synthetic hoon that produces a
dry `%lead` trap.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|?  p

##Wide form

|?(p)

##Irregular form

None

##Examples


    ~zod/try=> |?(20)
    < 1?lld
      [[[@da @ta] [@p @ta] *''] @n <250.yum 41.int 414.hhh 100.xkc 1.ypj %164>]
    >
    ~zod/try=> +:|?(20)
    ! -axis.3
    ! peek-park
    ! exit
    ~zod/try=> +:|.(20)
    [ [[~2014.10.22..19.39.41..0440 ~.~2014.10.22..19.39.41..0440] [~zod ~.~zod] <||>]
      ~
      <250.yum 41.int 414.hhh 100.xkc 1.ypj %164>
    ]

A lead core's payload cannot be read or written.

XX understand lead cores
