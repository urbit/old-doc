Ford
====

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
