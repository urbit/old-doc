Overview
===

Arvo is our operating system. 

[overview of how cards, etc get passed around]

Have you ever wondered what all these kernel modules are about?  What services
they provide?  What fundamental human desires they satisfy?  If so, this is the
doc for you!

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

- (&#37;ames)[vane/ames/overview.md] name of both our network and the vane that communicates over it
- (%clay)[vane/clay/overview.md] version-controlled, referentially- transparent, and global filesystem
- (%dill)[vane/dill/overview.md] terminal driver. Unix sends keyboard events to  %dill  from either the console or telnet, and  %dill  produces terminal output.
- (%eyre)[vane/eyre/overview.md] http server. Unix sends http messages to `%eyre`, and `%eyre` produces http messages in response
- (%ford)[vane/ford/overview.md] handles resources and publishing
- (%gall)[vane/gall/overview.md] manages our userspace applications.. `%gall` keeps state and manages subscribers
- (%time)[vane/time/overview.md] a simple timer 
