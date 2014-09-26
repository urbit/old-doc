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
          ;pre.gas: {<gas>}
        ==
      ==
    ==

Point a web browser at `http://ship-name.urbit.org/gen/main/pub/fab/ford/1/` to render the contents. Then try pointing your browser at `http://ship-name.urbit.org/gin/del/pub/fab/ford/1/`. 

What's going on?

We have introduced some new runes here, `/?`, `/=` and `/$`. These are a part of a whole family of runes that are especially relevant to writing content to the web. By convention, we indent four spaces after them.

`/?` simply checks for compatibility. In this case the line means 'need urbit 314 or below', or in hoon: `(lte zuse 314)`. `314` is the number in the kelvin versioning system, which you can read about [here](link).

`/=` is similar to the combination of `=+  =^`, or assignment. `/$` calls a parsing function on the location and remainder of the file. Here we use `++fuel`, found in `zuse.hoon`, to parse out some variables from the web request, and that's what we're writing to the page. 

Our page is made up of two generated parts: who requested the page, the location of the page and its revision. Both are parsed out of the `gas` variable using some standard library functions. We'll link to their documentation below. What's important to note is that `/=    gas  /$  fuel` is a pretty common way to open your page, since the product of `++fuel` is pretty useful when writing pages to the web.

Inside of the `;code` tag we also print (for reference) the entire `gas`, so you can take a look at the contents. This can be a helpful trick when debugging.

See also: `++ju`, `++spud` and `++scow`
