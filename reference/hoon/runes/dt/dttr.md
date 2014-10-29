#[dottar, `.*`, %dttr](#dttr)

[Short description]

#Syntax

`.*`, `dottr`, `[%dttr p=twig q=twig]` is a natural hoon that calculates the nock of subject `p`, formula `q`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

.*  p
q

##Wide form

.*(p q)

##Irregular form

None

##Examples

    ~zod/try=> .*([20 30] [0 2])
    20
    ~zod/try=> .*(33 [4 0 1])
    34
    ~zod/try=> .*(|.(50) [9 2 0 1])
    50
    ~zod/try=> .*(12 [7 [`1 [4 `1]] [`2 `3 `2]])
    [12 13 12]
    ~zod/try=> .*(~ [5 1^4 [4 1^3]])
    0
    ~zod/try=> .*(~ [5 1^5 [4 1^3]])
    1
