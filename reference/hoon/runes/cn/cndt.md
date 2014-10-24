#[cendot, `%.`, %cndt](#cndt)

Slam, reverse order

`%.` is a synthetic rune that reverses the order of [`%-`](). `%.` exists primarily for code readability and organization, see the [style guide]().

##Produces

Twig: `[%cndt p=twig q=twig]`

##Sample

`p` and `q` are [twig]()s.

##Tall form

    %.  p
        q

##Wide form

    %.(p q)

##Irregular form

None

##Examples

    ~zod/try=> %.(42 dec)
        41

In the above example, `%.` slams `++dec` with the sample `42`.

