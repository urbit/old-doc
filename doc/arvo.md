<div class="short">

# arvo Overview

arvo is our operating system.
It is a *structured* event system, designed to avoid the usual state of complex event networks: event spaghetti. We keep track of every event's cause
so that we have a clear causal chain for every computation.  At the bottom of every chain is a unix io event (e.g. network request, terminal input, file sync, timer event), and we push every step in the path the request takes is pushed onto the chain until we get to the immediate cause of the current computation. This causal stack routes results back to the caller.

















While we use arvo proper to route and control the flow of requests (%pass) and responses (%give) at a low level, arvo proper is rarely directly responsible for executing our desired end-computation (ie updating the state of an app). Instead, it passes off the request or response to one of its vanes, which each present an interface to clients for a particular well-defined, stable, and general-purpose piece of functionality.

As of this writing, we have seven vanes, which each provide the following services:

- [%ames](vane/ames/overview.md) name of both our network and the vane that communicates over it
- [%clay](vane/clay/overview.md) version-controlled, referentially- transparent, and global filesystem
- [%dill](vane/dill/overview.md) terminal driver. Unix sends keyboard events to `%dill` from either the console or telnet, and `%dill` produces terminal output.
- [%eyre](vane/eyre/overview.md) http server. Unix sends http messages to `%eyre`, and `%eyre` produces http messages in response
- [%ford](vane/ford/overview.md) handles resources and publishing
- [%gall](vane/gall/overview.md) manages our userspace applications.. `%gall` keeps state and manages subscribers
- [%time](vane/time/overview.md) a simple timer 

If we want to use the services of one of the vanes, we must append "%" and the first letter of the desired vane to the initial %pass. For example, if an app wants to send a request to another app, the arvo-specific portion of the request would look like this:

`[ost /*return-info-added-to-bone* %g ...]`

Above, ost is the bone, the path that follows is return information tacked onto the bone, and the %g informs arvo to send the request to %gall. To make this request complete, we would have two include two additional layers: the %gall-specific layer, for which we would use the %gall API defined in its ++kiss, and the app-specific layer, which we would use the API defined in its ++poke, ++peer, ..arms.


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
