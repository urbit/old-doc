1. 

Let's publish a web page. 

Create the file `/pub/fab/guide/exercise/1/hymn.hook` with the following contents:

    ;div
      ;h1: Exercise 1 — Simple HTML
      ;p: As you may notice, urbit has no problem talking to the web.
    ==

Save the file and navigate to `/gen/main/pub/fab/guide/five/exercise/1/`. 

What did you just do?

The code you just wrote is urbit's naitive programming langauge, hoon. Generating HTML with hoon is similar to writing [jade](link) or other similar HTML shorthand. In hoon, this shorthand is called `++sail`. 

In `++sail` node-names are prefixed with a `;` and closed with a `==`. Nodes that have text content and are only on one line use a `:` and are closed implicitly with a newl ine. Nodes with no content are closed with another `;`, such as `;br;`. 

When you need to you can find more information about `++sail` [here](link). 


2.

Let's do some programming on the page. 

Create the file `/pub/fab/guide/exercise/2/hymn.hook` with the following contents:

    ;div
      ;h1: Exercise 2 — Call a function
      ;p: Although it may be obvious, 2+2={<(add 2 2)>}
    ==

Save the file and navigate to `/gen/main/pub/fab/guide/five/exercise/2/`. 

What's going on there?

Clearly, the code `(add 2 2)` is generating `4`, and it's not too hard to see how. hoon, like lisp, is a functional language so you can try replacing `(add 2 2)` with `(add 2 (add 2 2))` to get a bit of a sense of it. In `++sail` we use `{` and `}` to do string interpolation. Everything after the `:` is considered a string, so we need to tell the parser when we start writing code again. The `<` and `>` are converting our result `4`, a number, to the string `"4"`. hoon is also a strongly typed language kind of like haskell. 