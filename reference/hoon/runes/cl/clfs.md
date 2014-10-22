#[colfas, `:/`, %clfs](#clfs)

[Short description]

#Syntax

`:/`, `colfas`, `[%clfs p=twig]` is a synthetic hoon that
produces `[%$ [%$ p ~] ~]`, ie, `[0 [0 p 0] 0]`.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

:/  p

##Wide form

:/(p)

##Irregular form

undefined

##Examples

    ~zod/try=> :/(20)
    [[%~. [%~. 20] ~] ~]
    ~zod/try=> :/(add 2 2)
    [[%~. [%~. 4] ~] ~]

Wraps twig in `[%$ [%$ .] ~]~`, used for interpolation.
