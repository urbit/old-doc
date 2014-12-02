(note to editor:  this is reasonably complete, particularly in terms of:  events
accepted by each vane, effects produced by each vane, and which vanes use which
other vanes)

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

As of this writing, we have seven vanes:  ames, clay, dill, eyre, ford, gall,
and time.  These are often prefixed by a cen, as in %ames.  We'll give here a
short description of the purpose and functionality of each of these vanes.

# Ames

Ames is the name of both our network and the vane that communicates over it.
When Unix receives a packet over the correct UDP port, it pipes it straight into
ames for handling.  Also, all packets sent over the ames network are sent by the
ames vane.  Apps and vanes may use ames to directly send messages to other
ships.  In general, apps use gall and clay to communicate with other ships
rather than using ames directly, but this isn't a requirement.  Of course, gall
and clay use ames behind the scenes to communicate across the network.  These
are the only two vanes that use ames.

Ames includes several significant components.  Although the actual crypto
algorithms are defined in zuse, they're used extensively in ames for encrypting
and decrypting packets.  Congestion control and routing is handled entirely in
ames.  Finally, the actual ames protocol itself, including how to route incoming
packets to the correct vane or app, is defined in ames.

# Clay

Clay is our filesystem.  Like any 21st century filesystem, it is
version-controlled, referentially-transparent, and global.  While this
filesystem is stored in clay, it is mirrored to Unix for convenience.  Unix
tells clays whenever a file changes in the Unix copy of the filesystem so that
the change may be applied.  Clay tells unix whenever an app or vane changes the
filesystem so that the change can be effected in Unix.  Apps and vanes may use
clay to write to the filesystem, query it, and subscribe to changes in it.
Ford and gall use clay to serve up apps and web pages.

Clay includes three components.  First is the filesystem/version control
algorithms, which are mostly defined in `++ze` and `++zu` in zuse.  Second is
the write, query, and subscription logic.  Finally, there is the logic for
communicating requests to, and receiving requests from, foreign ships.

# Dill

Dill is our terminal driver.  Unix sends keyboard events to dill from either the
console or telnet, and dill produces terminal output.  The only app that should
directly talk to dill is the terminal app.  Command-line apps are run by,
receive input from, and produce output to, the shell app, which is controlled by
terminal, which talks to dill, which talks to unix.  Clay also uses dill
directly to print out the filesystem change events, but this is questionable
behavior.

Dill has two main components.  First, it controls the terminal on a very basic,
event-by-event level.  This includes keeping track of things like the dimensions
of the terminal, the prompt type (plain text or password), which duct to produce
effects on, and so forth.  Second, it handles terminal events, keystroke by
keystroke.  Most characters are simply pushed onto the buffer and blitted to the
screen, but some characters, including control-modified keys, arrow keys, etc.
require special handling.  Most of the readline functionality is in dill.

# Eyre

Eyre is our http server.  Unix sends http messages to eyre, and eyre produces
http messages in response.  In general, apps and vanes do not call eyre; rather,
eyre calls apps and vanes.  Eyre uses ford and gall to functionally publish
pages and facilitate communication with apps.

Eyre primarily parses web requests and handles them in a variety of ways,
depending on the control string.  Nearly all of these are essentially stateless,
like functional publishing with ford.  Additionally, there's a fairly
significant component that handles gall messaging and subscriptions, which must
be stateful.

# Ford

Ford is our typed and marked computation engine.  A variety of different
services are provided by ford, but they mostly involve compiling hook files,
slapping/slammming code with marked data, and converting data between marks,
including validating data to a mark.  Throughout every computation, ford keeps
track of which resources are dependencies so that the client may be aware when
one or more dependencies are updated.

Ford neither accepts unix events nor produces effects.  It exists entirely for
the benefit of applications and other vanes, in particular gall.  Eyre exposes
the functional publishing aspects of ford while gall uses ford to control the
execution of applications.  Clay is intended to use ford to managed marked data,
but this is not yet reality.

# Gall

Gall manages our userspace applications.  It allows applications and vanes to
send messages to applications and subscribe to data streams.  This requires
gall to be a sort of a hypervisor.  Messages coming into gall are routed to the
intended application, and the response comes back along the same route.  If the
intended target is on another ship, gall will behind-the-scenes route it
through ames to the other ship to run.  This provides an abstraction where all
apps on all ships are communicated with over the same interface.

Gall neither accepts events from unix nor produces effects.  It exists entirely
for the benefit of other vanes and, in particular, applications.  Eyre exposes
gall's interface over http, and ames does the same over the ames network.  Gall
uses ford to compile and run the applications.

# Time

Time is a simple timer.  It allows vanes and applications to set and timer
events, which are managed in a simple priority queue.  Time produces effects to
start the unix timer, and when the requested time passes, unix sends wake events
to time, which time routes back to original sender.  We don't guarantee that a
timer event will happen at exactly the time it was set for, or even that it'll
be particularly close.  A timer event is a request to not be woken until after
the given time.

Eyre uses time for timing out sessions, and clay uses time for keeping track of
time-specified file requests.  Ames should probably use time to keep track of
things like network timeouts and retry timing, but it currently uses its own
alarm system.
