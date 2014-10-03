Reference
=========

Data Models
-----------

###`++axle`, formal state

```
++  axle                                                ::  all %ford state
  $:  %1                                                ::  version for update
      pol=(map ship baby)                               ::
  ==                                                    ::
```

This is the formal state of our vane.  Anything that must be remembered between
calls to ford must be stored here.  The number `%1` is a version number for our
state that allows us to upgrade the structure of our state in the future if we
wish.

`pol` is the a map from every ship on our pier to their individual ford state.
There is no shared ford state -- every ship is entirely separate.

###`++baby`, state by ship

```
++  baby                                                ::  state by ship
  $:  tad=[p=@ud q=(map ,@ud task)]                     ::  tasks by number
      dym=(map duct ,@ud)                               ::  duct to task number
      jav=(map ,* calx)                                 ::  cache
  ==                                                    ::
```

This is the state specific to each ship.

`tad` and `dym` keep track of the tasks we're currently working on.  `dym` is a
map from ducts to task numbers, and `q.tad` is a map from task number to the
task itself.  `p.tad` is the next available task number.  Thus, the keys of
`q.tad` are a subset of the numbers less than `p.tad`, and ford has attempted
exactly `p.tad` tasks so far.

`jav` is the cache of previously-solved problems.  The keys are a pair of a term
(either `%hood`, `%slap`, or `%slam`) and a noun that represents the exact
problem solved.  In the case of a `%hood`, then, the key is of the form `[%hood
beam cage]`.  For `%slap`, there is `[%slap vase twig]`.  For `%slam`, there is
`[%slam vase vase]`.  The values are the result of solving the problem.  Note
that this cache is wiped in `++stay` when ford is reloaded.

###`++task`, problem in progress

```
++  task                                                ::  problem in progress
  $:  nah=duct                                          ::  cause
      kas=silk                                          ::  problem
      kig=[p=@ud q=(map ,@ud beam)]                     ::  blocks
  ==                                                    ::
```

This is all the state we keep regarding a particular task.  `nah` is the duct
which asked us to solve the problem, and `kas` is the most recent statement of
the problem.

`kig` keeps track of which resources we are blocked on.  Our blocks are stored
by index in `q.kig`, and the next available index is `p.kig`.

###`++silk`, problem

```
++  silk                                                ::  construction layer
          $&  [p=silk q=silk]                           ::  cons
          $%  [%bake p=mark q=beam r=path]              ::  local synthesis
              [%boil p=mark q=beam r=path]              ::  general synthesis
              [%call p=silk q=silk]                     ::  slam
              [%cast p=mark q=silk]                     ::  translate
              [%done p=(set beam) q=cage]               ::  literal
              [%dude p=tank q=silk]                     ::  error wrap
              [%dune p=(set beam) q=(unit cage)]        ::  unit literal
              [%mute p=silk q=(list (pair wing silk))]  ::  mutant
              [%plan p=beam q=spur r=hood]              ::  structured assembly
              [%reef ~]                                 ::  kernel reef
              [%ride p=twig q=silk]                     ::  silk thru twig
              [%vale p=mark q=ship r=*]                 ::  validate [our his]
          ==                                            ::
```

This is the every type of problem we can solve.  Every `%exec` kiss that
requests us to solve a problem must choose one of these problems to solve.

Because this is both an internal structure used in ford and the public interface
to ford, we choose to document this structure in our discussion of the public
interface to ford below.

###`++calx`, cache line

```
++  calx                                                ::  concrete cache line
  $%  [%hood p=calm q=(pair beam cage) r=hood]          ::  compile
      [%slap p=calm q=[p=vase q=twig] r=vase]           ::  compute
      [%slam p=calm q=[p=vase q=vase] r=vase]           ::  compute
  ==                                                    ::
```

There are three kinds of cache entries.  Every entry includes some metadata in
`p` and is the combination of an input and its output.

The input to a `%hood` is the location of the resource and a cage representing
the data at that location.  The output is the hood found by compiling the given
cage at the given location.

The input to a `%slap` is the vase of the subject and the twig of the formula
against which we are slapping the subject.  The output is the vase produced by
slapping them.

The input to a `%slam` is the vase of the subject and the vase of the gate which
we are slapping.  The output is the vase produced by slamming them.

###`++calm`, cache line metadata

```
++  calm                                                ::  cache metadata
  $:  laz=@da                                           ::  last accessed
      dep=(set beam)                                    ::  dependencies
  ==                                                    ::
```

Every line in the cache needs to have two pieces of metadata.  We must know the
last time this line in the cache was accessed, and we must know what are the
dependencies of this line.

###`++hood`, assembly components

```
++  hood                                                ::  assembly plan
          $:  zus=@ud                                   ::  zuse kelvin
              sur=(list hoot)                           ::  structures
              lib=(list hoof)                           ::  libraries
              fan=(list horn)                           ::  resources
              src=(list hoop)                           ::  program
          ==                                            ::
```

When assembling a hook file, we split it into several sections.

`zus` is the kelvin version of the required zuse.  In general, we assume that
any newer (lower-numbered) zuse will retain backward compatibility, so any newer
zuse is also permissible.  This number is set with a `/?` at the beginning of
the file.

`sur` is the set of structures included.  These are included with the `/-` rune.
When a structure is included, we look in `/=main=/sur` for the given structure
and we load the gate there.  When compiling, all the included structures are
collected into a single core placed in the subject of the body with a `=>`.

`lib` is the set of librarires included.  These are included with the `/+` rune.
When a library is included, we look in `/=main=/lib` for the given library and
we load the library there.  As with structures, all the included libraries are
collected into a single core placed in the subject of the body with a `=>`.

`fan` is the set of resources included.  These are loaded in many different ways
and may load resources from any location.  These are placed in the subject of
the body with a `=~`.

`src` is the set of twigs or references to twigs in the body of the program.
Generally, each of these will represent a core, but this is not required.  When
compiling, these are strung together in a `=~`.

###`++hoot`

```
++  hoot  (pair bean hoof)                              ::  structure gate/core
```

A structures may be either a direct gate or a core.  These are syntactically
distinguished by adding a `*` to the beginning of the structure name for a core.
The structure itself is a `hoof`.

###`++hoof`

```
++  hoof  (pair term (unit (pair case ship)))           ::  resource reference
```

A hoof, which is either a structure or a library, has a name, and it may also
specify which version of the resource to use and which ship to retrieve it from.

###`++horn`

```
++  horn                                                ::  resource tree
          $%  [%ape p=twig]                             ::  /~  twig by hand
              [%arg p=twig]                             ::  /$  argument
              [%day p=horn]                             ::  /|  list by @dr
              [%dub p=term q=horn]                      ::  /=  apply face
              [%fan p=(list horn)]                      ::  /.  list
              [%for p=path q=horn]                      ::  /,  descend
              [%hub p=horn]                             ::  /@  list by @ud
              [%man p=(map span horn)]                  ::  /*  hetero map
              [%nap p=horn]                             ::  /%  homo map
              [%now p=horn]                             ::  /&  list by @da
              [%saw p=twig q=horn]                      ::  /;  operate on
              [%see p=beam q=horn]                      ::  /:  relative to
              [%sic p=tile q=horn]                      ::  /^  cast
              [%toy p=mark]                             ::  /mark/  static
          ==                                            ::
```

This is how we represent the static resources hook files can load.  The
discussion of their use from a user's perspective is documented elsewhere
(link), so we will here only give a description of the data structure itself.

A `%ape` horn is simply a twig that gets evaluated and placed in the subject.

A `%arg` is a gate that gets evaluated with a sample of our location and our
heel.

A `%day` is a horn that applies to each of a list of `@dr`-named files in the
directory.

A `%dub` is a term and horn, where the result of a horn is given the face of the
term.

A `%fan` is a list of horns, all at the current directory level.

A `%for` is a path and a horn, where the horn is evaluated relative to the given
path, where the given path is relative to the current location.

A `%hub` is a horn that applies to each of a list of `@ud`-named files in the
directory.

A `%man` is a map of spans to horns where the result is a set of each horn
applied to the current directory given the associated face.

A `%nap` is a homogenous map where each entry in a directory is handled with the
same horn and is given a face according to its name.

A `%now` is a horn that applies to each of a list of `@da`-named files in the
directory.

A `%saw` is a twig and a horn, where the twig operates on the result of the
horn.

A `%see` is a beam and a horn, where the horn is evaluated at a location of the
given beam.

A `%sic` is a tile and a horn, where the horn is evaluated and cast to the type
associated with the tile.

A `%toy` is simply a mark to be baked.

###`++hoop`, body

```
++  hoop                                                ::  source in hood
          $%  [%& p=twig]                               ::  direct twig
              [%| p=beam]                               ::  resource location
          ==                                            ::
```

This is an entry in the body of the hook file.  The hoop can either be defined
directly in the given file or it can be a reference to another file.  The second
is specified with a `//` rune.

###`++bolt`, monadic edge

```
++  bolt                                                ::  gonadic edge
  |*  a=$+(* *)                                         ::  product clam
  $:  p=cafe                                            ::  cache
    $=  q                                               ::
      $%  [%0 p=(set beam) q=a]                         ::  depends/product
          [%1 p=(set ,[p=beam q=(list tank)])]          ::  blocks
          [%2 p=(list tank)]                            ::  error
      ==                                                ::
  ==                                                    ::
```

Throughout our computation, we let our result flow through with the set of
dependencies of the value.  At various times, we may wish to either throw an
error or declare that the actual result cannot be found until a particular
resource is retrieved.  This is a perfect case for a monad, so here we define a
data structure for it.

At every step, we have a cache, so we store that in `p`.  In `q` we store the
data.

In the case of `%0`, we have the result in `q` and the set of dependencies in
`p`.

In the case of `%1`, we have a set of dependencies on which we are blocking.
When this happens, we make a call to clay to get the dependencies, and we
proceed with the computation when we receive them.  Technically, we restart the
computation, but since every expensive step is cached, there is no significant
performance penalty to doing this.  Referential transparency has its uses.

In the case of `%2`, we have a hit an error.  This gets passed all the way
through to the calling duct.  The list of tanks is some description of what went
wrong, often including a stack trace.

###`++burg`, monadic rule

```
++  burg                                                ::  gonadic rule
  |*  [a=$+(* *) b=$+(* *)]                             ::  from and to
  $+([c=cafe d=a] (bolt b))                             ::
::                                                      ::
```

To operate on bolts, we use `++cope` as our bind operator, and the functions it
works on are of type `burg`.  Our functions that operate on bolts should have a
sample of the cache and a value.  Their output should be a bolt of the output
value.  Then, `++cope` will only call the function when necessary (in the `%0`
case), and it will do so without the wrapping of a bolt.

If you understand monads, this is probably fairly obvious.  Otherwise, see the
discussion on `++cope` (link).

Public Interface
----------------

Ford does not export a scry interface, so the only way to interact with ford is
by sending kisses and receiving gifts.  In fact, ford only sends accepts one
kiss and gives one gift.  This is, of course, misleading because ford actually
does many different things.  It does, however, only produce one type of thing --
a result of a computation, which is either an error or the value produced along
with the set of dependencies referenced by it.

```
++  kiss                                                ::  in request ->$
          $%  [%exec p=@p q=(unit silk)]                ::  make / kill
          ==                                            ::
```

The `%exec` gift requests ford to perform a computation on behalf of a
particular ship.  `p` is the ship, and `q` is the computation.  If `q` is null,
then we are requesting that ford cancel the computation that it is currently
being run along this duct.  Thus, if you wish to cancel a computation, you must
send the kiss along the same duct as the original request.

Otherwise, we ask ford to perform a certain computation, as defined in `++silk`.
Since all computations produce the same type of result, we will discuss that
result before we jump into `++silk`.

```
++  gift                                                ::  out result <-$
          $%  [%made p=(each bead (list tank))]         ::  computed result
          ==                                            ::
```

We give either a `bead`, which is a result, or a list of tanks, which is an
error messge, often including a stack trace.

```
++  bead  ,[p=(set beam) q=cage]                        ::  computed result
```

This is a set of dependencies required to compute this value and a cage of the
result with its associated mark.

There are twelve possible computations defined in `++silk`.

```
++  silk                                                ::  construction layer
          $&  [p=silk q=silk]                           ::  cons
          $%  [%bake p=mark q=beam r=path]              ::  local synthesis
              [%boil p=mark q=beam r=path]              ::  general synthesis
              [%call p=silk q=silk]                     ::  slam
              [%cast p=mark q=silk]                     ::  translate
              [%done p=(set beam) q=cage]               ::  literal
              [%dude p=tank q=silk]                     ::  error wrap
              [%dune p=(set beam) q=(unit cage)]        ::  unit literal
              [%mute p=silk q=(list (pair wing silk))]  ::  mutant
              [%plan p=beam q=spur r=hood]              ::  structured assembly
              [%reef ~]                                 ::  kernel reef
              [%ride p=twig q=silk]                     ::  silk thru twig
              [%vale p=mark q=ship r=*]                 ::  validate [our his]
          ==                                            ::
```

First, we allow silks to autocons.  A cell of silks is also a silk, and the
product vase is a cell of the two silks.  This obviously extends to an arbitrary
number of silks.

`%bake` tries to functionally produce the file at a given beam with the given
mark and heel.  It fails if there is no way to translate at this level.

`%boil` functionally produces the file at a given beam with the given mark and
heel.  If there is no way to translate at this level, we descend recursively
into the path in the beam and attempt to translate there.  This should almost
always be called instead of `%bake`.

`%call` slams the result of one silk against the result of another.

`%cast` translates the given silk to the given mark, if possible.  This is one
of the critical and fundamental operations of ford.

`%done` produces exactly its input.  This is rarely used on its own, but many
silks are recursively defined in terms of other silks, so we often need a silk
that simply produces its input.  A monadic return, if you will.

`%dude` computes the given silk with the given tank as part of the stack trace
if there is an error.

`%dune` produces an error if the cage is empty.  Otherwise, it produces the
value in the unit.

`%mute` takes a silk and a list of changes to make to the silk.  At each wing in
the list we put the value of the associated silk.

`%plan` performs a structured assembly directly.  This is not generally directly
useful because several other silks perform supersets of this functionality.  We
don't usually have naked hoods outside ford.

`%reef` produces a core containing the entirety of zuse and hoon, suitable for
running arbitrary code against.  The mark is `%noun`.

`%ride` slaps a twig against a subject silk.  The mark of the result is `%noun`.

`%vale` validates untyped data from a ship against a given mark.  This is an
extremely useful function.

Commentary
==========

Parsing Hook Files
------------------

In the commentary on other vanes, we have traced through the lifecycle of
various external requests.  This is generally a very reasonable order to examine
vanes since it will eventually cover the entire vane, and we are never left
wondering why we are doing something.

For ford, however, it makes more sense to begin by discussing the parsing and
assembliing of hook files.  Many of the possible requests require us to assemble
hook files, so we may as well examine this immediately.

First, we will examine the parsing.  We parse a file at a beam to a hood in
`++fade:zo:za`.  The top-level parsing rule is `++fair`, which takes a beam and
produces a rule to parse an entire hood file.

A note on the naming scheme:  the parsing the combinators that parse into a
particular structure are conventionally given the same name as the structure.
Although this locally clobbers the type names, this pattern makes obvious the
intent of the parsing combinators.

We kick off with `++hood:fair`.

```
      ++  hood
        %+  ifix  [gay gay]
        ;~  plug
          ;~  pose
            (ifix [;~(plug fas wut gap) gap] dem)
            (easy zuse)
          ==
        ::
          ;~  pose
            (ifix [;~(plug fas hep gap) gap] (most ;~(plug com gaw) hoot))
            (easy ~)
          ==
        ::
          ;~  pose
            (ifix [;~(plug fas lus gap) gap] (most ;~(plug com gaw) hoof))
            (easy ~)
          ==
        ::
          (star ;~(sfix horn gap))
          (most gap hoop)
        ==
```

There are five sections to a hood:  system version, structures, libraries,
resources, and body.

First, we parse the requested version number of the system.  This is specified
with a unary `/?` rune.  If not present, then we default to the current version.

Second, we may have zero or more `/-` runes followed by a parsing of a `++hoot`,
which represents a shared structure.

Third, we may have zero or more `/+` runes followed by a parsing of a `++hoof`,
which represents a shared library.

Fourth, we may have zero or more other `/` runes (as described in `++horn`),
which represent program-specific resources to be loaded.

Fifth and finally, we must have one or more body statements (hoops), which are
either direct twigs or `//` runes.

```
      ++  hoot
        ;~  pose
          (stag %| ;~(pfix tar hoof))
          (stag %& hoof)
        ==
```

A structure can either be a direct gate, or it can be a simple core.  Either one
is parsed with `++hoof`, so we distinguish the two cases by requireing core
references to be prefixed by a `*`.

```
      ++  hoof
        %+  cook  |=(a=^hoof a)
        ;~  plug
          sym
          ;~  pose
            %+  stag  ~
            ;~(plug ;~(pfix fas case) ;~(pfix ;~(plug fas sig) fed:ag))
            (easy ~)
          ==
        ==
```

A hoof must have a name, which is a term.  Optionally, we also include a case
and a ship.  This is marked by appending a `/` followed by a case to denote the
requested version of the resource and a `/` followed by a ship name to denote
the requested source of the resource.  For example, `resource/1/~zod` requests
the first version of `resource` on `~zod`.

```
      ++  case
        %-  sear
        :_  nuck:so
        |=  a=coin
        ?.  ?=([%$ ?(%da %ud %tas) *] a)  ~
        [~ u=(^case a)]
```

Here, we parse a literal with `++nuck:so`, and we accept the input if it is
either an absolute date, an unsigned decimal, or a label.

This leaves only horns and hoops to parse.  Hoops are much simple to parse, so
we'll discuss those first.

```
      ++  hoop
        ;~  pose
          (stag %| ;~(pfix ;~(plug fas fas gap) have))
          (stag %& tall:vez)
        ==
```

There are two types of hoops.  Direct twigs are parsed with `++tall:vast`, which
is the just the hoon parser for a tall-form twig.

References to external twigs are marked with a `//` rune followed by a beam,
which is parsed with `++have`.

```
      ++  hath  (sear plex:voz (stag %clsg poor:voz))   ::  hood path
      ++  have  (sear tome ;~(pfix fas hath))           ::  hood beam
```

`++have` parses a path with `++hath`, and then it converts the path into a beam
with `++tome`.

`++hath` parses a `/`-separated list with `++poor:vast`, then converts it to an
actual path with `++plex:vast`.

This leaves only horns to parse.

```
      ++  horn
        =<  apex
        =|  tol=?
        |%
        ++  apex
          %+  knee  *^horn  |.  ~+
          ;~  pfix  fas
            ;~  pose
              (stag %toy ;~(sfix sym fas))
              (stag %ape ;~(pfix sig ape:read))
              (stag %arg ;~(pfix buc ape:read))
              (stag %day ;~(pfix bar day:read))
              (stag %dub ;~(pfix tis dub:read))
              (stag %fan ;~(pfix dot fan:read))
              (stag %for ;~(pfix com for:read))
              (stag %hub ;~(pfix pat day:read))
              (stag %man ;~(pfix tar man:read))
              (stag %nap ;~(pfix cen day:read))
              (stag %now ;~(pfix pam day:read))
              (stag %saw ;~(pfix sem saw:read))
              (stag %see ;~(pfix col see:read))
              (stag %sic ;~(pfix ket sic:read))
            ==
          ==
```

Horn parsing is slightly complex, so we create an internal core to organize our
code.  Our core has a global variable of `tol`, which is true if tall form is
permissible and false if we're already in wide form.  We kick off the parsing
with `++apex`.

`++apex` specifies how each rune is parsed.  This allows us to offload the
different ways of parsing the arguments to these runes into separate arms.  The
exception here is that the `%toy` horn is simply of the form `/mark/`.

We'll examine each of the horn parsing arms right after we discuss `++rail`,
which is used in each one.

```
        ++  rail
          |*  [wid=_rule tal=_rule]
          ?.  tol  wid
          ;~(pose wid tal)
```

This takes a wide-form and a tall-form parsing rule.  If tall form is
permissible, then it allows either rule to match; else, it allows only the wide
form rule.

```
        ++  read
          |%  ++  ape
                %+  rail
                  (ifix [sel ser] (stag %cltr (most ace wide:vez)))
                ;~(pfix gap tall:vez)
```

`++ape:read` parses for both the `/~` and the `/$` runes.  It produces a twig.
The wide form is a tuple of one or more ace-separated wide-form twigs parsed
with `++wide:vast` and surrounded by `[` and `]`.  The tall form is a single
tall form twig parsed by `++tall:vast`

```
              ++  day
                %+  rail
                  apex(tol |)
                ;~(pfix gap apex)
```

This parses for the `/|`, `/@`, `/%`, and `/&` runes.  It produces a horn.  The
wide form is, recursively, the entire horn parser with tall form disabled.  The
tall form is a gap followed by, recursively, the entire horn parser.

```
              ++  dub
                %+  rail
                  ;~(plug sym ;~(pfix tis apex(tol |)))
                ;~(pfix gap ;~(plug sym ;~(pfix gap apex)))
```

This parses for the `/=` rune.  It produces a term followed by a horn.  The wide
form is a symbol name followed by a `=` and, recursively, the entire horn parser
with tall form disabled.  The tall form is a gap followed by a symbol name,
another gap, and, recursively, the entire horn parser.

```
              ++  fan
                %+  rail  fail
                ;~(sfix (star ;~(pfix gap apex)) ;~(plug gap duz))
```

This parses for the `/.` rune.  It produces a list of horns.  There is no wide
form.  The tall form is a stet-terminated series of gap-separated recursive
calls to the entire horn parser.

```
              ++  for
                %+  rail
                  ;~(plug (ifix [sel ser] hath) apex(tol |))
                ;~(pfix gap ;~(plug hath ;~(pfix gap apex)))
```

This parses for the `/,` rune.  It produces a path and a horn.  The wide form is
a `[`-`]`-surrounded path followed by, recursively, the entire horn parser with
tall form disabled.  The tall form is a gap followed by a path, another gap,
and, recursively, the entire horn parser.

```
              ++  man
                %+  rail  fail
                %-  sear
                :_  ;~(sfix (star ;~(pfix gap apex)) ;~(plug gap duz))
                |=  fan=(list ^horn)
                =|  naf=(list (pair term ^horn))
                |-  ^-  (unit (map term ^horn))
                ?~  fan  (some (~(gas by *(map term ^horn)) naf))
                ?.  ?=(%dub -.i.fan)  ~
                $(fan t.fan, naf [[p.i.fan q.i.fan] naf])
```

This parses for the `/*` rune.  It produces a map of spans to horns.  There is
no wide form.  The tall form is a stet-terminated series of gap-separated
recursive calls to the entire horn parser.  All produced horns are expected to
be from `/=` runes.  The term and horn in each `/=` horn is inserted into the
produced map as a key-value pair.

```
              ++  saw
                %+  rail
                  ;~(plug ;~(sfix wide:vez sem) apex(tol |))
                ;~(pfix gap ;~(plug tall:vez ;~(pfix gap apex)))
```

This parses for the `/;` rune.  It produces a twig and a horn.  The wide form is
a wide-form twig followed by a `;` and, recursively, the entire horn parser with
tall form disabled.  The tall form is a gap followed by a tall-form twig,
another gap, and, recursively, the entire horn parser.

```
              ++  see
                %+  rail
                  ;~(plug ;~(sfix have col) apex(tol |))
                ;~(pfix gap ;~(plug have ;~(pfix gap apex)))
```

This parses for the `/:` rune.  It produces a beam and a horn.  The wide form is
a beam followed by a `;` and, recursively, the entire horn parser with tall form
disabled.  The tall form is a gap followed by a beam, another gap, and,
recursively, the entire horn parser.

```
              ++  sic
                %+  rail
                  ;~(plug ;~(sfix toil:vez ket) apex(tol |))
                ;~(pfix gap ;~(plug howl:vez ;~(pfix gap apex)))
          --
```

This parses for the `/^` rune.  It produces a tile and a horn.  The wide form is
a wide-form tile, parsed with `++toil:vast`, followed by a `^` and, recursively,
the entire horn parser with tall form disabled.  The tall form is a gap followed
by a tall-form tile, parsed with `++howl:vast`, another gap, and, recursively,
the entire horn parser.

Assembling Hook Files
---------------------

At this point, we've parsed a hook file into a hood.  We will now describe
exactly how this hood is assembled into a vase.  The problem of assembling is
handled entirely within the `++meow:zo:za` core.

```
    ++  meow                                            ::  assemble
      |=  [how=beam arg=heel]
      =|  $:  rop=(map term (pair hoof twig))           ::  structure/complex
              zog=(set term)                            ::  structure guard
              bil=(map term (pair hoof twig))           ::  libraries known
              lot=(list term)                           ::  library stack
              zeg=(set term)                            ::  library guard
              boy=(list twig)                           ::  body stack
              hol=?                                     ::  horns allowed?
          ==
      |%
```

We take two arguments and keep seven pieces of state.  `how` is the location of
the hook file we're assembling, and `arg` is the heel, or virtual path
extension, of the file.

In `rop`, we maintain a map of terms to pairs of hooves and twigs to represent
the structures we've encountered that we will put together in a core at the top
of the file.

In `zog`, we maintain the set of structures we're in the middle of loading.  If
we try to load a structure already in our dependency ancestry, then we fail
because we do not allow circular dependencies.  This enforces that our structure
dependency graph is a DAG.

In `bil`, we maintain a map of terms to pairs of hooves and twigs to represent
the libraries we've encountered that we will put together in a series of cores
after the structure core.

In `lot`, we maintain a stack of library names as they are encountered during a
depth-first search.  More precisely, we push a library onto the stack after
we've processed all its children.  Thus, every library depends only on things
deeper in the list.  The libraries must be loaded in the reverse of this order.
Concisely, this is a topological sort of the library dependency partial
ordering.

In `zeg`, we maintain the set of libraries we're in the middle of loading.  If
we try to load a library already in our dependency ancestry, then we fail
because we do not allow circular dependencies.  This enforces that our library
dependency graph is a DAG.

In `boy`, we maintain a stack of body twigs, which we'll put together in a
series of cores at the end of the file.

In `hol`, we decide if we're allowed to contain horns.  Libraries and structures
are not allowed to contain horns.

We in every case enter `++meow` through `++abut`.  You'll notice that there are
four (count 'em, four!) calls to `++cope` in `++abut`.  If you've glanced at the
ford code in general, you've probably seen cope over and over.  It is called in
79 different places.  We need to discuss the use of this critical function in
detail, so we may as well do it here.

```
    ++  cope                                            ::  bolt along
      |*  [hoc=(bolt) fun=(burg)]
      ?-  -.q.hoc
        %2  hoc
        %1  hoc
        %0  =+  nuf=(fun p.hoc q.q.hoc)
            :-  p=p.nuf
            ^=  q
            ?-  -.q.nuf
              %2  q.nuf
              %1  q.nuf
              %0  [%0 p=(grom `_p.q.nuf`p.q.hoc p.q.nuf) q=q.q.nuf]
      ==   ==
```

In monad-speak, this is the bind operator for the bolt monad.  If monads aren't
your thing, don't worry, we're going to explain the use of cope without further
reference to them.

Recall that there are three different types of bolt.  A `%2` error bolt contains
a list of tanks describing the error, a `%1` block bolt contains a set of
resources we're blocked on, and a `%0` value bolt contains an actual value and
the set of its dependencies.

We most commonly want to perform an operation on the value in a bolt if it is a
`%0` bolt.  If it's not a `%0` bolt, we want to leave it alone.  This requires
us to write a certain amount of boilerplate between each of our operations to
see if any of them produced a `%1` or a `%2` bolt.  This gets tiresome, so we
pull it out into a separate arm and call it `++cope`.

Intuitively, we're call the function `fun` with the value in `hoc`, where `fun`
takes an argument of type whatever is the value in a `%0` case of `hoc`, and it
produces a bolt of some (possibly different) type.  For brevity, we will refer
to the type of the of the value in the `%0` case of a bolt as the "type of the
bolt".

If the `hoc` bolt we're given as input to `fun` is already a `%1` or a `%2`
bolt, then we simply produce that.  We don't even try to run `fun` on it.

Otherwise, we run `fun` with the arguments from the bolt and, if it produces a
`%1` or a `%2` bolt, we simply produce that.  If it produces a `%0` bolt, then
we produce that with the old set of dependencies merged in with the new set.

We'll see more about how the bolt monad works as we run into more interesting
uses of it.  For now, this is sufficient to move on with `++abut`.

```
      ++  abut                                          ::  generate
        |=  [cof=cafe hyd=hood]
        ^-  (bolt vase)
        %+  cope  (apex cof hyd)
        |=  [cof=cafe sel=_..abut]
        =.  ..abut  sel
        %+  cope  (maim cof pit able)
        |=  [cof=cafe bax=vase]
        %+  cope  (chap cof bax [%fan fan.hyd])
        |=  [cof=cafe gox=vase]
        %+  cope  (maim cof (slop gox bax) [%tssg (flop boy)])
        |=  [cof=cafe fin=vase]
        (fine cof fin)
```

Our job is simple:  we must assemble a hood file into a vase.  Hopefully, the
usage of `++cope` is fairly understandable.  The correct way to read this is
that it does essentially five things.

First, we call `++apex` to process the structures, libraries, and body.  This
changes our state, so we set our context to the produced context.  Second, we
call `++able` to assemble the strucutres and libraries into a twig, which we
slap against zuse with `++maim`.  Third, we call `++chap` to process the
resources in the context of the already-loaded structures and libraries.
Fourth, we slap the body against the structures, libraries, and resources.
Fifth and finally, we produce the resultant vase.

```
      ++  apex                                          ::  build to body
        |=  [cof=cafe hyd=hood]
        ^-  (bolt ,_..apex)
        ?.  |(hol ?=(~ fan.hyd))
          %+  flaw  cof  :_  ~  :-  %leaf
          "horns not allowed in structures and libraries: {<[how arg]>}"
        %+  cope  (body cof src.hyd)
        |=  [cof=cafe sel=_..apex]
        =.  ..apex  sel
        %+  cope  (neck cof lib.hyd)
        |=  [cof=cafe sel=_..apex]
        =.  ..apex  sel(boy boy)
        %+  cope  (head cof sur.hyd)
        |=  [cof=cafe sel=_..apex]
        (fine cof sel)
```

First, we make sure that if we're not allowed to have horns, we don't.
Otherwise, we produce and error with `++flaw`.

```
++  flaw  |=([a=cafe b=(list tank)] [p=a q=[%2 p=b]])   ::  bolt from error
```

This produces a `%2` error bolt from a list of tanks.  Fairly trivial.

We should be starting to get used to the cope syntax, so we can see that we
really only do three things here.  We process the body with `++body`, the
libraries with `++neck`, and the structures with `++head`.

```
      ++  body                                          ::  produce functions
        |=  [cof=cafe src=(list hoop)]
        ^-  (bolt _..body)
        ?~  src  (fine cof ..body)
        %+  cope  (wilt cof i.src)
        |=  [cof=cafe sel=_..body]
        ^$(cof cof, src t.src, ..body sel)
```

We must process a list of hoops that represent our body.  If there are no more
hoops, we just produce our context in a `%0` bolt with `++fine`.

```
++  fine  |*  [a=cafe b=*]                              ::  bolt from data
          [p=`cafe`a q=[%0 p=*(set beam) q=b]]          ::
```

In monad-speak, this is the return operator.  For us, this just means that we're
producing a `%0` bolt, which contains a path and a set of dependencies.  We
assume there are no dependencies for the given data, or that they will be added
later.

If there are more hoops in `++body`, we call `++wilt` to process an individual
hoop and recurse.

```
      ++  wilt                                          ::  process body entry
        |=  [cof=cafe hop=hoop]
        ^-  (bolt _..wilt)
        ?-    -.hop
            %&  (fine cof ..wilt(boy [p.hop boy]))
            %|
          %+  cool  |.(leaf/"ford: wilt {<[(tope p.hop)]>}")
          %+  cope  (lend cof p.hop)
          |=  [cof=cafe arc=arch]
          ?:  (~(has by r.arc) %hoon)
            %+  cope  (fade cof %hoon p.hop)
            |=  [cof=cafe hyd=hood]
            %+  cope  (apex(boy ~) cof hyd)
            |=  [cof=cafe sel=_..wilt]
            (fine cof sel(boy [[%tssg boy.sel] boy]))
          =+  [all=(lark (slat %tas) arc) sel=..wilt]
          %+  cope
            |-  ^-  (bolt (pair (map term foot) _..wilt))
            ?~  all  (fine cof ~ ..wilt)
            %+  cope  $(all l.all)
            |=  [cof=cafe lef=(map term foot) sel=_..wilt]
            %+  cope  ^$(all r.all, cof cof, sel sel)
            |=  [cof=cafe rig=(map term foot) sel=_..wilt]
            %+  cope
              %=    ^^^^$
                  cof      cof
                  ..wilt   sel(boy ~)
                  s.p.hop  [p.n.all s.p.hop]
              ==
            |=  [cof=cafe sel=_..wilt]
            %+  fine  cof
            [`(map term foot)`[[p.n.all [%ash [%tssg boy.sel]]] lef rig] sel]
          |=  [cof=cafe mav=(map term foot) sel=_..wilt]
          ?~  mav
            (flaw cof [%leaf "source missing: {<(tope p.hop)>}"]~)
          (fine cof sel(boy [[%brcn mav] boy]))
        ==
```

In the case of a direct twig hoop, we just push it onto `boy` and we're done.
In the case of an indirect hoop, we must compile the referenced file.

First, we push onto the stack trace a message indicating which file exactly
we're compiling at the moment with `++cool`.

```
    ++  cool                                            ::  error caption
      |*  [cyt=trap hoc=(bolt)]
      ?.  ?=(%2 -.q.hoc)  hoc
      [p.hoc [%2 *cyt p.q.hoc]]
```

If an error occurred in computing `hoc`, we put the bunt of `cyt` onto the stack
trace.  Thus, `cyt` is not evaluated at all unless an error occurred.

Next in `++wilt`, we load the information about the filesystem node referenced
by the hoop with `++lend`.

```
    ++  lend                                            ::  load arch
      |=  [cof=cafe bem=beam]
      ^-  (bolt arch)
      =+  von=(ska %cy (tope bem))
      ?~  von  [p=cof q=[%1 [bem ~] ~ ~]]
      (fine cof ((hard arch) (need u.von)))
```

This is a simple call to the namespace.  If the resource does not yet exist, we
block on it by producing a `%1` bolt.  Otherwise, we cast it to an arch and
produce this.

Continuing in `++wilt`, we examine the produced arch.  If the referenced
filesystem node has a `hoon` child node, then we've found the required source,
so we parse it with `++fade`.  Recall that we referred earlier to `++fade`.  The
salient point there is that it takes a beam, reads in the hook file there, and
parses it into a hood file with `++fair`.

Now, we simply recurse on `++apex` to compile the new hood.  Note that, while we
do clear the `boy` list, we do not clear the other lists.  Thus, we are
accumulating all the structures and libraries referenced in all the referenced
hook files in one group, which we will put at the top of the product.

After this, we put the new list of body twigs into a `=~`, push this onto our
old list of body twigs, and produce the result.

If there is no hoon file here, then we descend into each of our children until
we find a hoon file.  First, we produce a list of all our children whose names
are terms with `++lark`.

```
++  lark                                                ::  filter arch names
  |=  [wox=$+(span (unit ,@)) arc=arch]
  ^-  (map ,@ span)
  %-  ~(gas by *(map ,@ span))
  =|  rac=(list (pair ,@ span))
  |-  ^+  rac
  ?~  r.arc  rac
  =.  rac  $(r.arc l.r.arc, rac $(r.arc r.r.arc))
  =+  gib=(wox p.n.r.arc)
  ?~(gib rac [[u.gib p.n.r.arc] rac])
```

We traverse the children map of `arc` to filter out those children whose names
aren't accepted by `wox` and produce a map from the product of `wox` to the
original name.  `++lark` is used in many cases to parse names into other types,
like numbers or dates, ignoring those which do not fit the format.  In `++wilt`,
though, we simply want to filter out those children whose names are not terms.

Next, we will produce a map from terms to feet.  Each of these feet will be
placed in a core named by the child name, and it will contain arms according to
its children.  Thus, if the indirect hoop references `/path`, then to access the
twig defined in `/path/to/twig/hoon`, our body must refer to `twig:to`.

If there are no more children, then we are done, so we produce our current
context.

Else, we recurse into the left and right sides of our map.  Finally, we process
our current entry in the map.  We first recurse by calling `++wilt` one level
down.  Thus, in the previous example, the first time we get to this point we are
processing `/path`, so we recurse on `++wilt` with path `/path/to`.  We also
remove our current body from the recursion, so that we may add it back in later
the way we want to.

After recursing, we push the new body onto our map, keyed by its name.  We also
produce the new context so that all external structures, libraries, and
resources are collected into the same place.

Finally, we have a map of names to feet.  If this map is empty, then there were
no twigs at the requested path, so we give an error with `++flaw`.

If the map is nonempty, then we finally produce our context with
with one thing pushed onto the front:  a core made out of the map we just
produced.

This concludes our discussion of `++wilt` and `++body`.  Thus, it remains in
`++apex` to discuss `++neck` and `++head`.

```
      ++  neck                                          ::  consume libraries
        |=  [cof=cafe bir=(list hoof)]
        ^-  (bolt ,_..neck)
        ?~  bir  (fine cof ..neck)
        ?:  (~(has in zeg) p.i.bir)
          (flaw cof [%leaf "circular library dependency: {<i.bir>}"]~)
        =+  gez=(~(put in zeg) p.i.bir)
        =+  byf=(~(get by bil) p.i.bir)
        ?^  byf
          ?.  =(`hoof`i.bir `hoof`p.u.byf)
            (flaw cof [%leaf "library mismatch: {<~[p.u.byf i.bir]>}"]~)
          $(bir t.bir)
        =+  bem=(hone %core %lib i.bir)
        %+  cope  (fade cof %hook bem)
        |=  [cof=cafe hyd=hood]
        %+  cope  (apex(zeg gez, hol |, boy ~) cof hyd)
        |=  [cof=cafe sel=_..neck]
        =.  ..neck
            %=  sel
              zeg  zeg
              hol  hol
              lot  [p.i.bir lot]
              bil  (~(put by bil) p.i.bir [i.bir [%tssg (flop boy.sel)]])
            ==
        ^^$(cof cof, bir t.bir)
```

Here, we're going to consume the list of libraries and place them in `bil`.  If
there are no more libraries, we're done, so we just produce our current context.

Otherwise, we check to see if the next library in the list is in `zeg`.  If so,
then this library is one of the libraries that we're already in the middle of
compiling.  There is a circular dependency, so we fail.

Otherwise, we let `gez` be `zeg` plus the current library so that while
compiling the dependencies of this library we don't later create a circular
dependency.  We check next to see if this library is alredy in `bil`.  If so,
then we have already included this library earlier, so we check to see if this
is the same version of the library as we included earlier.  If so, we skip it.
Else, we fail since we can't include two different versions of a library.  We
really should allow for newer versions of a library since in kelvin versioning
we assume backwards compatibility, but for now we require an exact match.

If we haven't already included this library, then we're going to do that.
First, we get the location of the library with `++hone`.

```
      ++  hone                                          ::  plant hoof
        |=  [for=@tas way=@tas huf=hoof]
        ^-  beam
        ?~  q.huf
          how(s ~[for p.huf way])
        [[q.u.q.huf %main p.u.q.huf] ~[for p.huf way]]
```

If we haven't specified the version of the library, we use the current ship,
desk, and case.  Otherwise, we use the given ship and case on desk `%main`.  In
either case, the path is `/way/p.huf/for`.  In the case of `++neck`, this means
`/lib/core/[library name]`.

In `++neck`, we next compile the hook file at that location with `++fade`.
Again, we will delay the discussion of `++fade`, noting only that it takes a
beam and parses the hook file there into a hood.

We recurse on this to compile the library.  During the compilation, we let `zeg`
be `gez` to avoid circular dependencies, we let `hol` be false since we don't
allow horns in libraries, and we let `boy` be null so that we can isolate the
new body twigs.

Next, we reintegrate the new data into our context.  We use the context created
by the recursion with four changes.  First, we reset `zeg` to our old `zeg`.
Second, we reset `hol` to our old `hol`.  Third, we put the name of our library
onto the stack of libraries.  This means all of a libraries dependencies will be
earlier in `lot` than the library itself, making `lot` a topological ordering on
the dependency graph.  Fourth, we put in `bil` the library hoof and body (with
all body twigs collected in a `=~`), keyed by the library name.

Finally, we recurse, processing the next library in our list.

To complete our disucssion of `++apex`, we must process our structures.

```
      ++  head                                          ::  consume structures
        |=  [cof=cafe bir=(list hoot)]
        |-  ^-  (bolt ,_..head)
        ?~  bir
          (fine cof ..head)
        ?:  (~(has in zog) p.q.i.bir)
          (flaw cof [%leaf "circular structure dependency: {<i.bir>}"]~)
        =+  goz=(~(put in zog) p.q.i.bir)
        =+  byf=(~(get by rop) p.q.i.bir)
        ?^  byf
          ?.  =(`hoof`q.i.bir `hoof`p.u.byf)
            (flaw cof [%leaf "structure mismatch: {<~[p.u.byf q.i.bir]>}"]~)
          $(bir t.bir)
        =+  bem=(hone ?:(p.i.bir %gate %core) %sur q.i.bir)
        %+  cope  (fade cof %hook bem)
        |=  [cof=cafe hyd=hood]
        %+  cope  (apex(zog goz, hol |, boy ~) cof hyd)
        |=  [cof=cafe sel=_..head]
        ?.  =(bil bil.sel)
          (flaw cof [%leaf "structures cannot include libraries: {<i.bir>}"]~)
        =.  ..head
            %=  sel
              boy  ?:  p.i.bir
                     boy
                   (welp boy [[[%cnzy p.q.i.bir] [%$ 1]] ~])
              zog  zog
              hol  hol
              rop  %+  ~(put by (~(uni by rop) rop.sel))
                      p.q.i.bir
                   [q.i.bir [%tssg (flop boy.sel)]]
            ==
        ^^$(cof cof, bir t.bir)
```

The processing of our structures is very similar to that of our libraries.  For
clarity, we'll use many of the same phrases in describing the parallel natures.
First, we check to see if there are more structures to process.  If not, we're
done, so we produce our context.

Otherwise, we let `goz` be `zog` plus the current structure so that while
compiling the dependencies of this structure we don't later create a circular
dependency.  We check next to see if this structure is alredy in `rop`.  If so,
then we have already included this structure earlier, so we check to see if this
is the same version of the structure as we included earlier.  If so, we skip it.
Else, we fail since we can't include two different versions of a structure.

If we haven't loaded this structure, then we call `++hone` to get the beam where
the file structure should be.  If the loobean in the hoot is true, then we're
looking for a gate; otherwise, we're looking for a core.  We parse this file
with `++fade`.

Now, we recurse on this to compile the structure.  During the recursion, there
we have threee changes.  Frist, we let `zog` be `goz` so that we don't create a
circular dependency.  Second, we let `hol` be false since we do not allow horns
in structures.  Third, we let `boy` be null so that we can isolate the new body
twigs.

Next, we reintegrate the new data into our context.  We use the context cretaed
by the recursion with four changes.  First, if we're including a gate structure,
then we reset the body to its original body.  Else we put on the top of our list
of body twigs what is essentially a `=+  structure-name` to take off the face of
the structure.  Second, we reset `zog` to our old `zog`.  Third, we reset `hol`
to our old `hol`.  Finally, we put in `rop` the structure hoof and body (with
all body twiggs collected in a `=~`), keyed by the structure name.

Finally, we recurse, processing the next structure in our list.

This concludes our discussion of `++apex`.

```
      ++  abut                                          ::  generate
        |=  [cof=cafe hyd=hood]
        ^-  (bolt vase)
        %+  cope  (apex cof hyd)
        |=  [cof=cafe sel=_..abut]
        =.  ..abut  sel
        %+  cope  (maim cof pit able)
        |=  [cof=cafe bax=vase]
        %+  cope  (chap cof bax [%fan fan.hyd])
        |=  [cof=cafe gox=vase]
        %+  cope  (maim cof (slop gox bax) [%tssg (flop boy)])
        |=  [cof=cafe fin=vase]
        (fine cof fin)
```

Returning to `++abut`, we have now processed the structures, libraries and body
twigs.  Next, we slap our preamble (structures and libraries) against zuse.
First, we construct our preamble in `++able`.

```
      ++  able                                          ::  assemble preamble
        ^-  twig
        :+  %tsgr
          ?:(=(~ rop) [%$ 1] [%brcn (~(run by rop) |=([* a=twig] [%ash a]))])
        [%tssg (turn (flop lot) |=(a=term q:(need (~(get by bil) a))))]
```

We first put the structures in `rop` into a single `|%` at the top and `=>` it
onto a `=~` of our libraries, in the reverse order that they appear in `lot`.
Thus, the structures are in a single core while the libraries are in consecutive
cores.

We slap the preamble against zuse with `++maim`.

```
    ++  maim                                            ::  slap
      |=  [cof=cafe vax=vase gen=twig]
      ^-  (bolt vase)
      %+  (clef %slap)  (fine cof vax gen)
      |=  [cof=cafe vax=vase gen=twig]
      =+  puz=(mule |.((~(mint ut p.vax) [%noun gen])))
      ?-  -.puz
        |  (flaw cof p.puz)
        &  %+  (coup cof)  (mock [q.vax q.p.puz] (mole ska))
           |=  val=*
           `vase`[p.p.puz val]
      ==
```

Here we start to get into ford's caching system.  We wrap our computation in a
call to `++clef` so that we only actually compute it if the result is not
already in our cache.  First we'll discuss the computation, then we'll discuss
the caching system.

We call `++mule` with a call to `++mint:ut` on the type of our subject vase
against the given twig.  In other words, we're compiling the twig with against
the subject type in the given subject vase.

If compilation fails, then we produce an error bolt with the produced stack
trace.  Otherwise, we run the produced nock with `++mock` and our sky function.
We convert the produced toon to a bolt with `++coup` and use the type from `puz`
combined with the value from `mock` to produce our vase.

If this process seems harder than just calling `++slap`, it's because it is.  We
have two requirements that `++slap` doesn't satisfy.  First, we want the to use
an explicit sky function for use with `.^`.  With `++slap`, you get whatever sky
function is available in the calling context, which in ford is none.  Second, we
want to explicitly handle the stack trace on failure.  `++slap` would cause
crash on failure.

We haven't yet discussed either `++clef` or `++coup`.  We'll start with `++coup`
to finish the discussion of the computation.

````
    ++  coup                                            ::  toon to bolt
      |=  cof=cafe
      |*  [ton=toon fun=$+(* *)]
      :-  p=cof
      ^=  q
      ?-  -.ton
        %2  [%2 p=p.ton]
        %0  [%0 p=*(set beam) q=(fun p.ton)]
        %1  ~&  [%coup-need ((list path) p.ton)]
            =-  ?-  -.faw
                  &  [%1 p=(sa (turn p.faw |=(a=beam [a *(list tank)])))]
                  |  [%2 p=p.faw]
                ==
            ^=  faw
            |-  ^-  (each (list beam) (list tank))
            ?~  p.ton  [%& ~]
            =+  nex=$(p.ton t.p.ton)
            =+  pax=(path i.p.ton)
            ?~  pax  [%| (smyt pax) ?:(?=(& -.nex) ~ p.nex)]
            =+  zis=(tome t.pax)
            ?~  zis
              [%| (smyt pax) ?:(?=(& -.nex) ~ p.nex)]
            ?-  -.nex
              &  [%& u.zis p.nex]
              |  nex
            ==
      ==
```

Recall that a toon is either a `%0` value, a `%1` block, or a `%2` failure.
Converting a `%2` toon failure into a `%2` bolt failure is trivial.  Converting
a `%0` toon value into a `%0` bolt value is easy since we assume there were no
dependencies.  Converting the blocks is rather more difficult.

To compute `faw`, we recurse through the list of paths in the `%1` toon.  At
each one, we make sure with `++tome` that it is, in fact, a beam.  If so, then
we check to see if the later paths succeed as well.  If so, we append the
current path to the list of other paths.  If not, we produce the error message
we got from processing the rest of the paths.  If this path is not a beam, then
we fail, producing a list of tanks including this path and, if later paths fail
too, those paths as well.

If some paths were not beams, then we produce a `%2` error bolt.  If all paths
were correct, then we produce a `%1` blocking bolt.

We will now discuss `++clef`.  This is where the cache magic happens.

```
    ++  clef                                            ::  cache a result
      |*  sem=*
      |*  [hoc=(bolt) fun=(burg)]
      ?-    -.q.hoc
          %2  hoc
          %1  hoc
          %0
        =^  cux  p.hoc  ((calk p.hoc) sem q.q.hoc)
        ?~  cux
          =+  nuf=(cope hoc fun)
          ?-    -.q.nuf
              %2  nuf
              %1  nuf
              %0
            :-  p=(came p.nuf `calx`[sem `calm`[now p.q.nuf] q.q.hoc q.q.nuf])
            q=q.nuf
          ==
        [p=p.hoc q=[%0 p=p.q.hoc q=((calf sem) u.cux)]]
      ==
```

If the value is already an error or a block, we just pass that through.
Otherwise, we look up the request in the cache with `++calk`.

```
++  calk                                                ::  cache lookup
  |=  a=cafe                                            ::
  |=  [b=@tas c=*]                                      ::
  ^-  [(unit calx) cafe]                                ::
  =+  d=(~(get by q.a) [b c])                           ::
  ?~  d  [~ a]                                          ::
  [d a(p (~(put in p.a) u.d))]                          ::
```

When looking up something in the cache, we mark it if we find it.  This way, we
have in our cache the set of all cache entries that have been referenced.  While
we do not at present do anything with this data, it should be used to clear out
old and unused entries in the cache.

Moving on in `++clef`, we check to see if we actually found anything.  If we
didn't find a cache entry, then we run the computation in `fun`, and examine its
result.  If it produced a `%2` error or `%1` block bolt, we just pass that
through.  Otherwise, we produce both the value and an updated cache with this
new entry.  We add the entry with `++came`.

```
++  came                                                ::
  |=  [a=cafe b=calx]                                   ::  cache install
  ^-  cafe                                              ::
  a(q (~(put by q.a) [-.b q.b] b))                      ::
```

We key cache entries by the type of computation (`-:calx`) and the inputs to the
computation (`q:calc`).  This just puts the cache line in the cache at the
correct key.

Back in `++clef`, if we did find a cache entry, then we just produce the value
at that cache line.  We convert the cache line into a value with `++calf`.

```
++  calf                                                ::  reduce calx
  |*  sem=*                                             ::  a typesystem hack
  |=  cax=calx
  ?+  sem  !!
    %hood  ?>(?=(%hood -.cax) r.cax)
    %slap  ?>(?=(%slap -.cax) r.cax)
    %slam  ?>(?=(%slam -.cax) r.cax)
  ==
```

This is simply a typesystem hack.  Because the `sem` is passed in through a wet
gate, we know at type time which of the three cases will be chosen.  Thus, the
correct type of the value in the cache line gets passed through to the caller.
This also depends on the fact that `++clef` is wet.  The type stuff here is
mathematically interesting, but the action is simple:  we get the value from the
cache line.

This concludes our discussion of `++clef` and `++maim`.

Back in `++abut`, recall that we processed the structures, libraries, and body
with `++apex`.  Then, we slapped our preamble (structures and libraries) against
zuse with `++maim`.  Next, we process our resources with `++chap`.  Note that we
pass in the preamble so that we may refer to anything in there in our resources.

`++chap` is broken up into a different case for each horn.  We'll go through
them one by one.

```
      ++  chap                                          ::  produce resources
        |=  [cof=cafe bax=vase hon=horn]
        ^-  (bolt vase)
        ?-    -.hon
            %ape  (maim cof bax p.hon)
```

This is `/~`.  We slap the twig against our context.

```
            %arg
          %+  cope  (maim cof bax p.hon)
          |=  [cof=cafe gat=vase]
          (maul cof gat !>([how arg]))
```

This is `/$`.  We slap the twig against our context, which we expect to produce
a gate.  We slam this gate with a sample of `how` and `arg`, which is our
location and the heel (virtual path extension).

`++maul` is similar to `++maim`, but it slams instead of slaps.

```
    ++  maul                                            ::  slam
      |=  [cof=cafe gat=vase sam=vase]
      ^-  (bolt vase)
      %+  (clef %slam)  (fine cof gat sam)
      |=  [cof=cafe gat=vase sam=vase]
      =+  top=(mule |.((slit p.gat p.sam)))
      ?-  -.top
        |  (flaw cof p.top)
        &  %+  (coup cof)  (mong [q.gat q.sam] (mole ska))
           |=  val=*
           `vase`[p.top val]
      ==
```

We cache slams exactly as we cache slaps.  We use `++slit` to find the type of
the product of the slam given the types of the gate and the sample.

If this type fails, we produce the given stack trace as a `%2` error bolt.
Otherwise, we produce the top produced above combined with the value we get from
slamming the values in the vases with  `++mong`.

Back to `++chap`.

```
            %day  (chad cof bax %dr p.hon)
```

This is `/|`.  We call `++chad` to convert textual names to relative dates and
process the next horn against each of the discovered paths.

```
      ++  chad                                          ::  atomic list
        |=  [cof=cafe bax=vase doe=term hon=horn]
        ^-  (bolt vase)
        %+  cope  ((lash (slat doe)) cof how)
        |=  [cof=cafe yep=(map ,@ span)]
        =+  ^=  poy  ^-  (list (pair ,@ span))
            %+  sort  (~(tap by yep) ~)
            |=([a=[@ *] b=[@ *]] (lth -.a -.b))
        %+  cope
          |-  ^-  (bolt (list (pair ,@ vase)))
          ?~  poy  (fine cof ~)
          %+  cope  $(poy t.poy)
          |=  [cof=cafe nex=(list (pair ,@ vase))]
          %+  cope  (chap(s.how [q.i.poy s.how]) cof bax hon)
          |=  [cof=cafe elt=vase]
          (fine cof [[p.i.poy elt] nex])
        |=  [cof=cafe yal=(list (pair ,@ vase))]
        %+  fine  cof
        |-  ^-  vase
        ?~  yal  [[%cube 0 [%atom %n]] 0]
        (slop (slop [[%atom doe] p.i.yal] q.i.yal) $(yal t.yal))
```

First, we call `++lash` to parse the children of the current beam and pick out
those ones that are of the requested format.

```
    ++  lash                                            ::  atomic sequence
      |=  wox=$+(span (unit ,@))
      |=  [cof=cafe bem=beam]
      ^-  (bolt (map ,@ span))
      %+  cope  (lend cof bem)
      |=  [cof=cafe arc=arch]
      (fine cof (lark wox arc))
```

First, we get the arch with `++lend`, as described above.  We filter and parse
the child names with `++lark` according to the given parser function.

In `++chad`, this parser function is `(slat doe)`, which will parse a cord into
an atom of the requested odor.  For `%day` the odor is for relative dates.

Thus, we now have a map from atoms of the given odor to the actual child names.
We next turn this map into a list and sort it in increasing order by the atom.

We next convert this list of pairs of atoms and spans to a list of pairs of
atoms and vases.  We process the given horn once at every child beam, producing
the resource at that location.

Finally, we convert this list of pairs of atoms and vases to a vase of a list of
pairs of atoms to (well-typed) values.  Each entry in the list is of type atom
with the given odor combined with the type of the produced vase.

Back in `++chap`, we continue parsing resources.

```
            %dub
          %+  cope  $(hon q.hon)
          |=  [cof=cafe vax=vase]
          (fine cof [[%face p.hon p.vax] q.vax])
```

This is `/=`.  We process the given horn, giving us a vase.  We put as a face on
the vase so that it may be referred to later by name.

```
            %fan
          %+  cope
            |-  ^-  (bolt (list vase))
            ?~  p.hon  (fine cof ~)
            %+  cope  ^$(hon i.p.hon)
            |=  [cof=cafe vax=vase]
            %+  cope  ^$(cof cof, p.hon t.p.hon)
            |=  [cof=cafe tev=(list vase)]
            (fine cof [vax tev])
          |=  [cof=cafe tev=(list vase)]
          %+  fine  cof
          |-  ^-  vase
          ?~  tev  [[%cube 0 [%atom %n]] 0]
          (slop i.tev $(tev t.tev))
```

This is `/.`.  We first process each of the child horns, producing a list of
vases.  This is done by just recursing on `++chap`.  Then, we simply fold over
this list to create a vase of the list of values.

```
            %for  $(hon q.hon, s.how (weld (flop p.hon) s.how))
```

This is `/,`.  We simply recurse on the horn with the given path welded onto our
current beam.

```
            %hub  (chad cof bax %ud p.hon)
```

This is `/@`.  This is exactly like the processing of `%day` except we expect
the children to be named as unsigned integers rather than relative dates.  We
process the horn at each of the children's locations and produce a list of pairs
of absolute dates and values.

```
            %man
          |-  ^-  (bolt vase)
          ?~  p.hon  (fine cof [[%cube 0 [%atom %n]] 0])
          %+  cope  $(p.hon l.p.hon)
          |=  [cof=cafe lef=vase]
          %+  cope  ^$(cof cof, p.hon r.p.hon)
          |=  [cof=cafe rig=vase]
          %+  cope  ^^^$(cof cof, hon q.n.p.hon)
          |=  [cof=cafe vax=vase]
          %+  fine  cof
          %+  slop
            (slop [[%atom %tas] p.n.p.hon] vax)
          (slop lef rig)
```

This is `/*`.  We process each of the horns in the given map by recursion
through `++chap`.  Once we have these vases, we create a vase of a map from the
given textual names to the produced values.

```
            %now  (chad cof bax %da p.hon)
```

This is `/&`.  This is exactly like the processing of `%now` except we expect
the children to be names as absolute dates rather than relative dates.  We
process the horn at each of the children's locations and produce a list of pairs
of absolute dates and values.

```
            %nap  (chai cof bax p.hon)
```

This is `/%`.  Here, we process the horn at each of our children with `++chai`.

```
      ++  chai                                          ::  atomic map
        |=  [cof=cafe bax=vase hon=horn]
        ^-  (bolt vase)
        %+  cope  (lend cof how)
        |=  [cof=cafe arc=arch]
        %+  cope
          |-  ^-  (bolt (map ,@ vase))
          ?~  r.arc  (fine cof ~)
          %+  cope  $(r.arc l.r.arc)
          |=  [cof=cafe lef=(map ,@ vase)]
          %+  cope  `(bolt (map ,@ vase))`^$(cof cof, r.arc r.r.arc)
          |=  [cof=cafe rig=(map ,@ vase)]
          %+  cope  (chap(s.how [p.n.r.arc s.how]) cof bax hon)
          |=  [cof=cafe nod=vase]
          (fine cof [[p.n.r.arc nod] lef rig])
        |=  [cof=cafe doy=(map ,@ vase)]
        %+  fine  cof
        |-  ^-  vase
        ?~  doy  [[%cube 0 [%atom %n]] 0]
        %+  slop
          (slop [[%atom %a] p.n.doy] q.n.doy)
        (slop $(doy l.doy) $(doy r.doy))
```

We get the arch at our current beam with `++lend`.  Then, we process the horn at
each of our children to give us a map of atoms to vases.  Finally, we convert
that into a vase of a map of these atoms to the values.  This is very similar to
`++chad` and the handling of `%man`.

```
            %see  $(hon q.hon, how p.hon)
```

This is `/:`.  We process the given horn at the given beam.

```
            %saw
          %+  cope  $(hon q.hon)
          |=  [cof=cafe sam=vase]
          %+  cope  (maim cof bax p.hon)
          |=  [cof=cafe gat=vase]
          (maul cof gat sam)
```

This is `/;`.  First, we process the given horn.  Then, we slap the given twig
against our context to produce (hopefully) a gate.  Finally, we slam the vase
we got from processing the horn against the gate.

```
            %sic
          %+  cope  $(hon q.hon)
          |=  [cof=cafe vax=vase]
          %+  cope  (maim cof bax [%bctr p.hon])
          |=  [cof=cafe tug=vase]
          ?.  (~(nest ut p.tug) | p.vax)
            (flaw cof [%leaf "type error: {<p.hon>} {<q.hon>}"]~)
          (fine cof [p.tug q.vax])
```

This is `/^`.  First, we process the given horn.  Then, we slap the the bunt of
the given tile against our context.  This will produce a vase with the correct
type.  We test to see if this type nests within the type of the vase we got from
processing the horn.  If so, we produce the value from the horn along with the
type from the tile.  Otherwise, we produce a `%2` error bolt.

```
            %toy  (cope (make cof %bake p.hon how ~) feel)
        ==
```

This is `/mark/`.  Here, we simply run the `%bake` silk on the given mark,
producing a cage.  We convert this cage into a vase with `++feel`, which is
exactly as simple as it sounds like it should be.

```
++  feel  |=([a=cafe b=cage] (fine a q.b))              ::  cage to vase
```

This is trivial.

We will discuss later `++make` and how `%bake` is processed.  Suffice it to say
that baking a resource with a given mark gets the resource and converts it, if
necessary, to the requested mark.

This concludes our discussion of `++chap`.

We return once more to `++abut`.

```
      ++  abut                                          ::  generate
        |=  [cof=cafe hyd=hood]
        ^-  (bolt vase)
        %+  cope  (apex cof hyd)
        |=  [cof=cafe sel=_..abut]
        =.  ..abut  sel
        %+  cope  (maim cof pit able)
        |=  [cof=cafe bax=vase]
        %+  cope  (chap cof bax [%fan fan.hyd])
        |=  [cof=cafe gox=vase]
        %+  cope  (maim cof (slop gox bax) [%tssg (flop boy)])
        |=  [cof=cafe fin=vase]
        (fine cof fin) 
```

Recall that we processed our structures, libraries and body with `++apex`.  We
slapped our structures and libraries against zuse with `++maim`.  We processed
our resources with `++chap`.  Now, all our body twigs are collected in a `=~` and
slapped against our structures, libraries, and resources.  This produces our
final result.

The hook file has been assembled.  And there was great rejoicing.

Lifecycle of a Kiss
-------------------

We're now going to go through a series of lifecycle descriptions.  When a user
of ford sends a kiss, it is once of a dozen different types of silk.  We'll go
through each one, tracing through the flow of control of each of these.

First, though, we'll describe the common handling to all kisses.


Lifecycle of a `%bake`
----------------------

Lifecycle of a `%done`
----------------------

```
          %done  [cof %0 p.kas q.kas]
```

This is trivial.  We simply produce the given cage with the given set of
dependencies.  This is used when we already have a cage that we want to insert
into another silk that requires a silk argument.  It's analogous to the return
operator in a monad -- which makes it sound way more complicated than it is.

Lifecycle of a `%dude`
----------------------

```
          %dude  (cool |.(p.kas) $(kas q.kas))
```

This simply puts a given tank on the stack trace if the given silk produces an
error.  This is implemented as a simple call to `++cool`.

Lifecycle of a `%dune`
----------------------

```
          %dune
        ?~  q.kas  [cof [%2 [%leaf "no data"]~]]
        $(kas [%done p.kas u.q.kas])
```

This is a sort of a `++need` for silks.  If there is no data in the unit cage,
we produce an error.  Else, we simply produce the data in the cage.

Lifecycle of a `%plan`
----------------------

```
          %plan  
        %+  cope  (abut:(meow p.kas q.kas) cof r.kas)
        |=  [cof=cafe vax=vase]
        (fine cof %noun vax)
```

This is a direct request to compile a hood at a given beam with a heel of the
given path.  We comply by calling `++abut` with the given arguments and
producing the vase with a mark of `%noun`.

Lifecycle of a `%reef`
----------------------

```
          %reef  (fine cof %noun pit)
```

This is one of the simplest silks.  We simply produce our context, which is zuse
compiled against hoon.  The mark is a `%noun`.
