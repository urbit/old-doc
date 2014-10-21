#[sigpam, `~&`, %sgpm](#sgpm)

[Short description]

#Syntax

`~&`, `sigpam`, `[%sgpm p=@ud q=twig r=twig]` is a synthetic hoon 
that prints `q` on the console before computing `r`.  `p` is the
log priority, 0-3 defaulting to 0.

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

Priority 0 (debug):

    ~&  q
    r

Priority 1 (notice):

    ~&  >  q
    r

Priority 2 (warning):

    ~&  >>  q
    r

Priority 3 (alarm):

    ~&  >>>  q
    r

##Wide form

~&(>> q r)

##Irregular form

undefined

##Examples

undefined

