#buccom `$,` %bccm

Normalizing gate (or [clam]())

`$,` is a synthetic rune that produces a normalizing gate [clam]() for `p`. `$,` is used to ensure an input value fits a certain type:if it does match, the value is produced. If it doesn't, the default value for the desired type is produced.

##Produces

[Twig](): `[%bccb p=tile] `

##Sample

`p`  is a [tile]()

##Tall form

    $,  p

##Wide form

None

##Irregular form

    ,p

##Examples

    ++  cord  ,@t                                           ::  text atom (UTF-8)

In `++cord`, `,` creates a gate that validates atoms of the odor [`@t`]().

