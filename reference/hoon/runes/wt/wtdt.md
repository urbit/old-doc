#[wutdot, `?.`, %wtdt](#wtdt)

[Short description]

#Syntax

`?.`, `wutdot`, `[%wtdt p=twig q=twig r=twig]` is a synthetic hoon
that produces `r` if `p` is yes (`&`, `0`), or `q` if `p` is no
(`|`, 1).


See also `?:`

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

?.  p
      q
    r

##Wide form

?:(p q r)

##Irregular form

None

##Examples

    ~zod/try=> ?.((gth 1 2) 1 2)
    1
    ~zod/try=> ?.(?=(%a 'a') %not-a %yup)
    %yup
