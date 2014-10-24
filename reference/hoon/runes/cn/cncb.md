#[cencab, `%_`, %cncb](#cncb)

Evaluate with changes, cast

`%_` is a synthetic rune that evaluates `p` with the changes specified in `q`, then casts the product back to the type of `p`. `%_` is used to change a batch of [face]()s inside a [`++wing`]() all at once, ensuring that the product is type checked.

##Produces

Twig: `[%cncb p=wing q=tram]`

##Sample

`p` is a [`++wing`](), a list of [`++limb`]()s.
`q` is a [`++tram`](), a list of [`++wing`]()s and twigs.

##Tall form

    %_  p
          p.i.q  q.i.q
          p.i.t.q  q.i.t.q
        ==

##Wide form

    %_(p p.i.q q.i.q, p.i.t.q q.i.t.q)

##Irregular form

None

##Examples

    /~zod/try=> =a [b=1 c=2 d=3]
    new var %a
    /~zod/try=> %_(a b (add 3 b.a), c (add 3 c.a), d (add 3 d.a))
    [b=4 c=5 d=6]

Here we're using `%_` to add 3 to all of the values inside of our shell variable `a`.

    /~zod/try=> =a [b='odors' c='twigs' d='tiles']
    changed %a
    /~zod/try=> %_(a b c.a, c d.a, d b.a)
    [b='twigs' c='tiles' d='odors']

In this case we're using `%_` to swap the values of the faces in `a`.