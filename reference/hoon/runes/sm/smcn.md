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

    ~zod/try=> 
    ;=
      ;%  |=(a=marl (turn a |=(b=manx ;script(src (poxo b));)))
      ; /gep/hart.js
      ; /gen/main/lib/urb.js
      ; //cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.js
    ==
    ~[
      [[%script [%src "/gep/hart.js
    "] ~] ~]
      [[%script [%src "/gen/main/lib/urb.js
    "] ~] ~]
      [ [ %script
          [%src "//cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.js
    "]
          ~
        ]
        ~
      ]
    ]
    ~zod/try=> 
    %-  many:poxo  :_  ~
    ;=
      ;%  |=(a=marl (turn a |=(b=manx ;script(src (poxo b));)))
      ; /gep/hart.js
      ; /gen/main/lib/urb.js
      ; //cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.js
    ==
    "<script src="/gep/hart.js"></script><script src="/gen/main/lib/urb.js"></script><script src="//cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.js"></script>" 
