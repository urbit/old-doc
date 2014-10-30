#[semlus, `;+`](#smls)

[Short description]

#Syntax

`;+`, `semlus`, is a virtual hoon that is used within [sail] to interpolate in a
manx.

##Produces

Affects surrounding manx

##Sample

`p` is a twig

##Tall form

;+  a

##Wide form

Within quoted form, 

`+{a}` or `{a}`

##Irregular form

None

##Examples

    ~zod/try=> ;div  ;+  ;hi;
               ==
    [[%div ~] [[%hi ~] ~] ~]
    ~zod/try=> ;div:"+{;hi;}"
    [[%div ~] [[%hi ~] ~] ~]
    ~zod/try=> (poxo ;div:"+{;hi;}")
    "<div><hi></hi></div>"
