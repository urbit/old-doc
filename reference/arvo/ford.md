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



###`++hoop`

```
++  hoop                                                ::  source in hood
          $%  [%& p=twig]                               ::  direct twig
              [%| p=beam]                               ::  resource location   
          ==                                            ::
```

This is an entry in the body of the hook file.  The hoop can either be defined
directly in the given file or it can be a reference to another file.  The second
is specified with a `//` rune.
