#[semcen, `;%`](#smcn)

`++sail` interpolate tape

`;%` is a virtual rune used within [`++sail`]() for passing a list of child nodes to a gate. `;%` is used for transforming a list of child elements inside a [`++manx`]().

##See also

The `%e` case inside of [`++tuna`]().

##Produces

Twig: [`++marl`]()

##Sample

`p` is a [twig]().

##Tall form

    ;%  p

##Wide form

    %{p}

(within quoted form)

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
