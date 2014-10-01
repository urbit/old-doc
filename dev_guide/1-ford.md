1.

In an editor open `/main/pub/fab/guide/ford/1/hymn.hook`. It should look like this:

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

Point a web browser at `http://ship-name.urbit.org/gen/main/pub/fab/ford/1/` to render the contents. Then try pointing your browser at `http://ship-name.urbit.org/gin/del/pub/fab/ford/1/`. 

What's going on?

In short, we're printing out some of the parameters our page is passed: who is looking at it, where it is and what revision its on. We have also thrown in all our parameters in a codeblock for reference.

To do this we have introduced some new runes, `/?`, `/=` and `/$`. We tend to call runes with a leading `/` "`%ford` runes" since they are used by the `%ford` vane for resource loading and composition. By convention, we indent four spaces after them to make them more obvious. They belong at the top of the file.

** Link to %ford overview

`/?` simply checks for compatibility. In this case the line means 'need urbit 314 or below', or in hoon: `(lte zuse 314)`. `314` is the number in the kelvin versioning system, which you can read about [here](link). 

`/=` is similar to the combination of `=+  =^`, or assignment. `/$` calls a parsing function (`++fuel` in `zuse.hoon`) with the `++beam` and `++path` of our current file. `/=    gas  /$  fuel` is a  common way to open your page, since the product of `++fuel` is useful when writing pages to the web. The use of `++fuel` is not enforced, and you can also write your own parser. 

** Explain what ++beam and ++path are
** "/=  gas  /$  fuel" is the same as setting gas to the result of (fuel beam path).
** This could be the point to talk about %clay
**THIS PROCESS IS UNCLEAR, BOTH IN WHAT IT DOES AND HOW ITS DONE**

Our page is made up of two generated parts: who requested the page, the location of the page and its revision. Both are parsed out of the `gas` variable using some straightforward library functions, [`++ju`](link), [`++spud`](link) and [`++scow`](link). You can follow those links to the library reference to learn more about them.  Inside of the `;code` tag we also print (for reference) the entire `gas`, so you can take a look at the contents. This can be a helpful trick when debugging. To fully understand what gets put in `gas`, we can take a look at `++fuel` and note that it produces a [`++epic`](link), which also contains a [`++cred`](link). You can follow those links to learn more about them.  When we try changing the url from `gen/main` to `gin/del/main` we're using some of the access methods from `%eyre` to pretend to be the carrier `~del`. You can find documentation on those access methods in the `%eyre` commentary, [here](link).  Path and identity are useful, but there are some other parameters worth checking out as well.  2.  In an editor open `/main/pub/fab/guide/ford/2/hymn.hook`. It should look like this: :: :: ::::  /hook/hymn/five/guide/fab/pub/ :: /?    314 /=    gas  /$  fuel :: ^-  manx ;html ;head ;title: %ford Example 2 == ;body ;div: Do you have a code?  ;div: ?code={<(fall (~(get by qix.gas) %code) '')>} == == Point a web browser at `http://ship-name.urbit.org/gen/main/pub/fab/ford/2/` to render the contents. Then try pointing your browser at `http://ship-name.urbit.org/gen/main/pub/fab/ford/2/?code=1618`.  What's going on?  This is a simple example, showing off another use of `/=    gas  /$  fuel`. In this simple example we're just pulling out the value of the `code` url parameter. You should be able to change that value to any url-safe string and see it appear on the page. We're using a few simple library functions to actually pull the value out, [`++fall`](link) and [`get:by`](link).  3.  In an editor open `/main/pub/fab/guide/ford/3/hymn.hook`. It should look like this: :: :: ::::  /hook/hymn/five/guide/fab/pub/ :: /?    314 /=    gas  /$  fuel
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

Also open `/main/pub/fab/guide/ford/3/lib.hook`. It should look like this:

    |%
    ++  fib  |=(x=@ ~+(?:((lth x 2) 1 (add $(x (dec x)) $(x (sub x 2))))))
    --

Try pointing a web browser at `https://ship-name.urbit.org/gen/main/pub/fab/ford/3/` to render the output.

How is this getting put together?

In this example we're loading a library and calling a function from that library. The library is simple, containing only one function, that computes the Fibonacci number of a number. 

To do this we have introduced a new rune, `//`, which can be used to load local resources. We are using the relative path `/%%/lib` to load our `lib.hook` file. The context of this file is `/hymn/hook`, so we use `%%` to go up one level in the same way you would use `..`. For more about paths, see [arvo basics](link).

`//` is only one of a family of runes used for resource loading. In our next example we'll explore some others.



