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
              bil=(map term (pair hoof twig))           ::  libraries known
              lot=(list term)                           ::  library stack
              zeg=(set term)                            ::  library guard
              boy=(list twig)                           ::  body stack
          ==
      |%
```

We take two arguments and keep five pieces of state.  `how` is the location of
the hook file we're assembling, and `arg` is the heel, or virtual path
extension, of the file.

In `rop`, we maintain a map of terms to pairs of hooves and twigs to represent
the structures we've encountered that we will put together in a core at the top
of the file.

In `bil`, we maintain a map of terms to pairs of hooves and twigs to represent
the libraries we've encountered that we will put together in a series of cores
after the structure core.

In `lot`, we maintain a stack of library names in the order they are encounterd
during a depth-first search.  Thus, every library depends only on things later
in the list.  The libraries must be loaded in the reverse of this order.  Note
that this only maintains the list of libraries in the ancestry of the current
library load.  XX check

In `zeg`, we maintain a set of libraries already loaded.  If we try to load a
library already loaded in our ancestry, then we fail because we do not allow
circular dependencies.  This combined with `lot` enforce that our library
dependency graph is a DAG while not restricting us to a tree.  XX check

In `boy`, we maintain a stack of body twigs, which we'll put together in a
series of cores at the end of the file.

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

