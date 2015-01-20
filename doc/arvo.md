<div class="short">

# arvo Overview

arvo is our operating system.
It is a *structured* event system, designed to avoid the usual state of complex
event networks: event spaghetti. We keep track of every event's cause so that
we have a clear causal chain for every computation.  At the bottom of every
chain is a unix io event (e.g. network request, terminal input, file sync,
timer event), and we push every step in the path the request takes is pushed
onto the chain until we get to the immediate cause of the current computation.
This causal stack routes results back to the caller.

This causal stack is called a `++duct`.  This is represented simply as a list of
paths, where each path represents a step in the causal chain.  The first element
in the path is the first letter of whichever vane handled that step in the
computation, or the empty span for unix.  Here's a duct that was recently
observed in the wild:

```
~[
  /g/a/~zod/4_shell_terminal/u/time
  /g/a/~zod/shell_terminal/u/child/4/main
  /g/a/~zod/terminal/u/txt
  /d/term-mess
  //term/1
]
```

This is the duct the timer vane receives when "timer" sample app asks the timer
vane to set a timer.  This is also the duct over which the response is produced
at the specified time.  Unix sent a terminal keystroke event (enter), and arvo
routed it to dill, which passed it on to the gall app terminal, which sent it to
shell, its child, which created a new child (with process id 4), which on
startup asked the timer vane to set a timer.

The timer vane saves this duct, so that when the specified time arrives and unix
sends a wakeup event to the timer vane, it can produce the response on the same
duct.  This response is routed to the place we popped off the top of the duct,
i.e. the time app.  This app produces the text "ding", which falls down to the
shell, which drops it through to the terminal.  Terminal drops this down to
dill, which converts it into an effect that unix will recognize as a request to
print "ding" to the screen.  When dill produces this, the last path in the duct
has an initial element of the empty span, so this is routed to unix, which
applies the effects.

If your mind is screaming "call stack" at you, you're following along well.
This is a call stack, with a crucial feature:  the stack is a first-class
citizen.  You can respond over a duct zero, one, or many times.  You can save
ducts for later use.  There are definitely parallels to Scheme-style
continuations, but simpler and with more structure.

<goto-gosub paragraph>

If ducts are a call stack, then how do we make calls and produce results?  Arvo
processes moves, which are a combination of message data and metadata.  There
are two types of moves.  A `%pass` move is analogous to a call:

```
[duct %pass return-path=path vane-name=@tD data=card]
```

Arvo pushes the return path (preceded by the first letter of the vane name) onto
the duct and sends the given data to the vane we specified.  Any response will
come along the same duct with the path `return-path`.

A `%give` move is analogous to a return:

```
[duct %give data=card]
```

Arvo pops the top path off the duct and sends the given data to it.


 TRANSITION TO BONES


--more on what kind it is (functional, event driven)
--the consequences of this.

[overview of how cards, etc get passed around]

The basic purpose of a vane is to present an interface to clients for some
well-defined, stable, and general-purpose piece of functionality.  There are
three types of clients:  Unix, apps, and other vanes.  They all communicate
using a message-passing system we call the "card" system, which you may or may
not have read about elsewhere in our docs.  Unix, apps, and vanes send cards to
each other in message-passing style to communicate.  All meaningful
communication happens through these messages.  Thus, anything you might want to
do with a vane is exposed through its definition of `++kiss`, which defines the
types of cards it accepts.

As of this writing, we have seven vanes:  `%ames`, `%clay`, `%dill`, `%eyre`,
`%ford`, `%gall`, and `%time`. 

- [%ames](vane/ames/overview.md) name of both our network and the vane that communicates over it
- [%clay](vane/clay/overview.md) version-controlled, referentially- transparent, and global filesystem
- [%dill](vane/dill/overview.md) terminal driver. Unix sends keyboard events to `%dill` from either the console or telnet, and `%dill` produces terminal output.
- [%eyre](vane/eyre/overview.md) http server. Unix sends http messages to `%eyre`, and `%eyre` produces http messages in response
- [%ford](vane/ford/overview.md) handles resources and publishing
- [%gall](vane/gall/overview.md) manages our userspace applications.. `%gall` keeps state and manages subscribers
- [%time](vane/time/overview.md) a simple timer 

</div>
