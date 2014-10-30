#[semhep, `;-`](#smhp)

[Short description]

#Syntax

`;-`, `semhep`, is a virtual hoon that is used within [sail] to interpolate in a
tape.

##Produces

Affects surrounding manx

##Sample

`p` is a twig

##Tall form

;-  a

##Wide form

Within quoted form, 

`-{a}` or `{a}`

##Irregular form

None

##Examples

    ~zod/try=> ;div  ;-  "hi"
               ==
    [[%div ~] [[%~. [%~. "hi"] ~] ~] ~]
    ~zod/try=> ;div:"-{"hi"}"
    [[%div ~] [[%~. [%~. "hi"] ~] ~] ~]
    ~zod/try=> (poxa ;div:"-{"hi"}")
    "<div>hi</div>"
