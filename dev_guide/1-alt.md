1. 

Let's publish a webpage

In
    /pub/fab/guide/exercise/1/hymn.hook

Put

    ;div
      ;h1: Exercise 1 — Simple HTML
      ;p: As you may notice, urbit has no problem talking to the web.
    ==

Try it

    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/1/

What did you just do?

The code you just wrote is urbit's naitive programming langauge, hoon. Generating HTML with hoon is similar to writing [jade](link) or other similar HTML shorthand. In hoon, this shorthand is called `++sail` and it's a naitive part of the hoon language.

In `++sail` node-names are prefixed with a `;` and closed with a `==`. Nodes that have text content and are only on one line use a `:` and are closed implicitly with a new line. Nodes with no content are closed with another `;`, such as `;br;`. 

When you need to you can find more information about `++sail` [here](link). 


2.

Let's do some programming on the page. 

In
    /pub/fab/guide/exercise/2/hymn.hook

Put

    ;div
      ;h1: Exercise 2 — Call a function
      ;p: Although it may be obvious, 2+2={<(add 2 2)>}
    ==

Try it
    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/2/

What's going on there?

Clearly, the code `(add 2 2)` is generating `4`, and it's not too hard to see why. `add` is one of the library functions that are a part of `hoon.hoon`. Try replacing `(add 2 2)` with `(sub 2 2)`. You can find documentaiton for the full hoon library in the [library reference](link) if you're interested. 

Since the product of `(add 2 2)` is a number, we need a few extra things to have it print properly. In `++sail` we use `{` and `}` to do string interpolation. Everything after the `:` is considered a string, so we need to tell the parser when we start writing code again. The `<` and `>` are converting our result `4`, a number, to the string `"4"`. hoon is a strongly typed language kind of like haskell. 


3. 

Let's assign some variables.

In
    /pub/fab/guide/exercise/3/hymn.hook

Put
    =+  a=2
    =+  ^=  b  (add 2 2)
    ;div
      ;h1: Exercise 3 — Assignment
      ;p: a={<a>}
      ;p: b={<b>}
      ;p: a+b={<(add a b)>}
    ==

Try it
    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/3/

How does that work?

The first thing you should notice in this example is the `=+` at the top of our file. `=+` is a rune. hoon is a programming with no reserved words. No `if` `this` or `function` at all. Instead, runes have their own pronunciation. `=+` is pronounced 'tislus'. You can find the table of pronunciation [here](link). In hoon you construct your programs using runes, which are two character ascii pairs. You can see the whole set of runes in the [rune index](link).

`=+` pushes an expression on to our subject. The subject in hoon is something like `this` in other languages. hoon being a functional language if we want something to be available further on in our computation we need to attach it to the subject first. 

Looking at the rendered page it's clear that we're assigning `a` to be `1` and `b` to be `2`. Looking at the code, however, you can see that we're doing this in two different ways. Runes in hoon can have irregular forms, and `^=` is one of them. The first two lines of our example are doing the same thing, where `a=2` is simply the irregular form of `^=  a  2`. You can see the full list of irregular forms [here](link).


4. 

Let's build our own computation

In
    /pub/fab/guide/exercise/4/hymn.hook

Put
    |%
      ++  start  1
      ++  end  10
      ++  length
        |=
          [s=@ud e=@ud]
        (sub end start)
    --
    ;div
      ;h1: Exercise 4 — Cores
      ;p: We'll be starting at {<start>}
      ;p: And ending at {<end>}
      ;p: Looks like a length of {<(length start end)>}
    ==

Try it
    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/4/

What's happening?

As you can see from the output, we have written a little function that takes two numbers, `s` and `e`   and returns their difference. The first thing to notice about our code is the first rune. `|%` is a `core` rune. You can think of cores like functions or objects in other languages. `|%` runes contain an arbitrary number of arms, denoted with either `++` or `+-` and closed with `--`. 

Each arm has a value, either static data (in the case of `++start` and `++end`) or a gate (in the case of `++length`). A gate is a kind of core. Gates only have one arm and are quite similar to a function in other languages. We use `|=` to construct our gate. Runes in hoon are generally categorized by their first character. `|` indicates a rune having to do with cores. You can find all of the `|` runes in the [rune library](link).

Our `++length` gate takes two arguments, `s` and `e`. In hoon we call the data passed in to a gate the 'sample'. Every `|=` has two parts, the sample type and the computation also known as a `tile` and a `twig`. Casually, `[s=@ud e=@ud]` means that the gate takes two arguments, labelled going forward as `s` and `e`, and required to both be `@ud` or unsigned decimal. Our computation, `(sub e s)` simply computes the difference between `e` and `s`. 

`@ud` is an odor. Odors aren't quite types, but they're similar. You'll learn the difference by example as we progress, and you can always refer to the [odor index](link). 

You probably also noticed our indentation. In general hoon has both tall and wide forms. In general, we use tall form when programming and wide form in the REPL. In wide form, hoon uses two spaces for indentation and is back-stepped so nested code doesn't drift away toward the right margin. 


5.

In
    /pub/fab/guide/exercise/5/hymn.hook

Put
    |%
      ++  dist  ,[start=@ud end=@ud]
      ++  length
        |=
          [d=dist]
        (sub end.d start.d)
    --
    ;div
      ;h1: Cores
      ;p: How long does it take to get from 2 to 20? {<(length [2 20])>}
    ==

Try it
    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/5/

What's the difference?

Clearly we're producing the same result as before, but we're doing it in a different way. 

The first line in our gate, `++length` always specifies the sample tile. As you can see here, our sample tile is actually a `++dist`, the body of which, `,[start=@ud end=@ud]` looks very similar to our previous example in that it accepts two `@ud`. The important difference is that `++dist` is now defined in a way that can be re-used. hoon is a strongly typed language, but it encourages the creation of your own types using what we call tiles.

At a high level you can think of hoon as being composed of two things, tiles and twigs. Twigs are the actual AST structures that get consumed by the compiler. Tiles reduce to twigs and provide major affordances for the programmer. If you're interested in learning about tiles more deeply you can find an in-depth explanation in the [tile section](link).

It should suffice, for now, to say that we create tiles in the same way that you would think of creating type definitions in another language. Some of those types are actually built in, and you can find more about them in the [`$` rune library](link). 

In this specific example we are using the `$,` tile rune in its irregular form, `,`. `,` generates a validator from the given expression. In effect, `++dist` uses the type system to only produce cells that appear in the form `[start=@ud end=@ud]`. When we use it in our `++length` gate we assert that our input must be validated by `++dist`. As we continue you'll see how this pattern can be quite useful.

One other thing to point out which may be immediately confusing coming from other languages is the order of addressing `start` and `end`. We call these labels faces, and we address them in the opposite order. You can read more about how faces work in the commentary on `++type` [here](link).


6.

In
    /pub/fab/guide/exercise/6/hymn.hook

Put
    ::
    ::
    ::::  /hook/hymn/6/exercise/guide/fab/pub/
      ::
    /?    314
    /=    gas  /$  fuel
    ::
    ^-  manx
    ;html
      ;head
        ;title: %ford Example 1
      ==
      ;body
        ;div.who: {<(~(get ju aut.ced.gas) 0)>}
        ;div.where: {(spud s.bem.gas)} rev {(scow %ud p.r.bem.gas)}
        ;code
          ;pre: {<gas>}
        ==
      ==
    ==

Try it
    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/5/
    http://talsur-todres.urbit.org/gin/del/main/pub/fab/guide/exercise/5/

We're printing out some of the parameters our page is passed: who is looking at it, where it is and what revision our desk is on. We have also thrown in all our FCGI parameters in a codeblock for reference.

To do this we have introduced some new runes, `/?`, `/=` and `/$`. We tend to call runes with a leading `/` "`%ford` runes" since they are used by the `%ford` vane for resource loading and composition. By convention, we indent four spaces after them to make them more obvious. They belong at the top of the file.

`/?` simply checks for compatibility. In this case the line means 'need urbit 314 or below', or in hoon: `(lte zuse 314)`. `314` is the number in the kelvin versioning system, which you can read about [here](link). 

`/=` is similar to the combination of `=+  =^`, or assignment. `/$` calls a parsing function, which we specify as [`++fuel`](link) with the [`++beam`](link) and [`++path`](link) of our current file. `/=    gas  /$  fuel` is a  common way to open your page, since the product of `++fuel` is useful when writing pages to the web. The use of `++fuel` is not enforced — you can also write your own parser. 

Our page is made up of two generated parts: who requested the page, the location of the page and its revision. Both are parsed out of the `gas` variable using some straightforward library functions, [`++ju`](link), [`++spud`](link) and [`++scow`](link). You can follow those links to the library reference to learn more about them. You'll also notice our addressing moving in the opposite direction as you may be used to. `aut.ced.gas` pulls `aut` from inside `ced` from inside `gas`. 

Inside of the `;code` tag we also print (for our own reference) the entire `gas`, so you can take a look at the contents. This can be a helpful trick when debugging. To fully understand what gets put in `gas`, we can take a look at `++fuel` and note that it produces a [`++epic`](link), which also contains a [`++cred`](link). You can follow those links to learn more about them.

When we try changing the url from `gen/main` to `gin/del/main` we're using some of the access methods from `%eyre` (the urbit webserver) to pretend to be the carrier `~del`. You can find documentation on those access methods in the `%eyre` commentary, [here](link). 

Path and identity are useful, but there are some other parameters worth checking out as well.

7.

In
    /pub/fab/guide/exercise/7/hymn.hook

Put
    ::
    ::
    ::::  /hook/hymn/five/guide/fab/pub/
      ::
    /?    314
    /=    gas  /$  fuel
    ::
    ^-  manx
    ;html
      ;head
        ;title: %ford Example 2
      ==
      ;body
        ;div: Do you have a code?
        ;div: ?code={<(fall (~(get by qix.gas) %code) '')>}
      ==
    ==

Try it
    http://ship-name.urbit.org/gen/main/pub/fab/guide/exercise/7/
    http://ship-name.urbit.org/gen/main/pub/fab/guide/exercise/7//?code=yes-i-do

This is a simple example, showing off another use of `/=    gas  /$  fuel`. In this simple example we're just pulling out the value of the `code` url parameter. You should be able to change that value to any url-safe string and see it appear on the page. 

We're using a few simple library functions to actually pull the value out, [`++fall`](link) and [`get:by`](link). URL parameters are stored in `qix.gas` as a `++map`, one of the main container constructs used in hoon. We'll encounter a lot of maps along the way, and you can learn more about them in the [map section](link) of the library doc.


8.

In
    /pub/fab/guide/exercise/8/hymn.hook

Put
    ::
    ::
    ::::  /hook/hymn/five/guide/fab/pub/
      ::
    /?    314
    /=    gas  /$  fuel
    |%
    ++  fib  
      |=  x=@
        ?:  (lth x 2)
          1
        (add $(x (dec x)) $(x (sub x 2)))
    --
    ::
    ^-  manx
    ;html
      ;head
        ;title: %ford Example 3
      ==
      ;body
        ;div: {<(~(get by qix.gas) %number)>}
      ==
    ==

Try it
    http://ship-name.urbit.org/gen/main/pub/fab/guide/exercise/8/


9.

In
    /pub/fab/guide/exercise/9/hymn.hook

Put
    ::
    ::
    ::::  /hook/hymn/five/guide/fab/pub/
      ::
    /?    314
    /=    gas  /$  fuel
    ::
    //    /%%/lib
    ^-  manx
    ;html
      ;head
        ;title: %ford Example 3
      ==
      ;body
        ;div: {<(fib 30)>}
      ==
    ==

And in
    /pub/fab/guide/exercise/9/lib.hook

Put
    ++  fib  
      |=  x=@
        ?:  (lth x 2)
          1
        (add $(x (dec x)) $(x (sub x 2)))
    --

Try it
    http://ship-name.urbit.org/gen/main/pub/fab/guide/exercise/9/

