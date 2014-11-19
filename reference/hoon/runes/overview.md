#Overview

In Hoon there are no reserved words. Instead, [`++twigs`]() (abstract syntax trees), are formed using a diagraph of two ASCII symbols, which is called a rune. 

For instance, the rune `?:`, pronounced "wutcol", is a rune that accepts three [`++twig`] expressions to form an "if-then-else statement," where `p` is the predicate, `q` is the "then" statement, and `r` is the "else" statement:

        [%wtcl p=twig q=twig r=twig] 

In a program, it is used like so:

    ++  add
        |=  [a=@ b=@]
        ^-  @
        ?:  =(0 a)  b
        $(a (dec a), b +(b))          

Here the `=(0 a)` is `p`, the `b` is `q`, and the bottom line is the `r`.

There are several benefits to using runes in lieu of reserved words. First, it prevents the programmer from accidentally misusing a reserved word as a variable name, which also allows her to be sure that any word in her progam is an identifier. Next, as the first ASCII symbol of the rune digraphs bears semantic significance, the programmer can look at any rune and immediately have a basic, intuitive understanding as to what it does. Furthermore, runes produce cleaner code. For example, here is the C equivalent of the `++add` source code printed above:

    attribute add {
         function(left-operand: atom, right-operand: atom)
         produce atom
         if equals(0, left-operand) {
          right-operand
         } else {
            recurse(left-operand (decrement left-operand)), 
                    right-operand (increment right-operand))
         }
       } 

Lastly, but perhaps most significantly, code is meant to be seen, and not read. Anyone who has even slight experience coding Hoon will tell you that they can understand and connect with properly formatted Hoon code on a deeper, more intuitive level that cannot be explained but must be experienced. One doesn't read `++add`, she sees it.

###The categories


