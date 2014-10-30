#[semcen, `;%`](#smcn)

[Short description]

#Syntax

`;%`, `semcen`, is a virtual hoon that is used within [sail] to interpolate in a
tape.

##Produces

Affects surrounding manx

##Sample

`p` is a twig

##Tall form

;%  a

##Wide form

Within quoted form, 

`%{a}` or `{a}`

##Irregular form

None

##Examples

    ~zod/try=> ;div  ;%  |=(a=marl (weld a a))
               ;hi;
               ; foo
               ;p;
    ==
    [ [%div ~]
      ~[
        [g=[n=%hi a=~] c=~]
        [g=[n=%$ a=~[[n=%$ v="""
                             foo
                             """]]] c=~]
        [g=[n=%p a=~] c=~]
        [g=[n=%hi a=~] c=~]
        [g=[n=%$ a=~[[n=%$ v="""
                             foo
                             """]]] c=~]
        [g=[n=%p a=~] c=~]
      ]
    ]
    ~zod/try=> ;div:"%{|=(a=marl (weld a a))};{hi}foo;{p}"
    [ [%div ~]
      ~[
        [g=[n=%hi a=~] c=~]
        [g=[n=%$ a=~[[n=%$ v="foo"]]] c=~]
        [g=[n=%p a=~] c=~]
        [g=[n=%hi a=~] c=~]
        [g=[n=%$ a=~[[n=%$ v="foo"]]] c=~]
        [g=[n=%p a=~] c=~]
      ]
    ]
    ~zod/try=> (poxo ;div:"%{|=(a=marl (weld a a))};{hi}foo;{p}")
    "<div><hi></hi>foo<p></p><hi></hi>foo<p></p></div>"
