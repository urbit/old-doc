#[semtar, `;*`](#smtr)

[Short description]

#Syntax

`;*`, `semtar`, is a virtual hoon that is used within [sail] to interpolate in a
marl.

##Produces

Affects surrounding manx

##Sample

`p` is a twig

##Tall form

;*  a

##Wide form

Within quoted form, 

`*{a}` or `{a}`

##Irregular form

None

##Examples

    ~zod/try=> ;div:"*{~[;hi; ;p;]}"
    [[%div ~] [[%hi ~] ~] [[%p ~] ~] ~]
    ~zod/try=> ;div:"a*{~[;hi; ;p;]}b"
    [ [%div ~]
      [[%~. [%~. "a"] ~] ~]
      [[%hi ~] ~]
      [[%p ~] ~] 
      [[%~. [%~. "b"] ~] ~]
      ~
    ]
    ~zod/try=> (poxo ;div:"a*{~[;hi; ;p;]}b")
    "<div>a<hi></hi><p></p>b</div>"
