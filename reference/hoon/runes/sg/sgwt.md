#[sigwut, `~?`, %sgwt](#sgwt)

[Short description]

#Syntax

`~?`, `sigwut`, `[%sgwt p=@ud q=twig r=twig s=twig]` is a
synthetic hoon with the same hint effect, printing `r`,
as `[%sgpm p r s]`, iff `q` produces yes.

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

None

##Examples

    ~zod/try=> ~?((gth 1 2) 5 ~)
    ~
    ~zod/try=> ~?((gth 1 0) 5 ~)
    5
    ~
