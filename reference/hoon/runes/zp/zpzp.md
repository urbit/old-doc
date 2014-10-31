#[zapzap, `!!`, %zpzp](#zpzp)

[Short description]

#Syntax

    ++  twig  
      $%  [%zpzp p=~]
      ==

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

None

##Wide form

!!

##Irregular form

None

##Examples

Frequently used as sentinel

    ~zod/try=> !!
    ! exit
    ~zod/try=> =|(a=(unit) ?^(a !! %none))
    %none
    ~zod/try=> :type; =|(a=(unit) ?^(a !! %none))
    %none
    %none
    ~zod/try=> ?+('a' !! %a 1, %b 2)
    1
    ~zod/try=> ?+('c' !! %a 1, %b 2)
    ! exit
