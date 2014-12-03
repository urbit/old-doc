Overview 
===

`%ford` is our typed and marked computation engine.  A variety of different
services are provided by `%ford`, but they mostly involve compiling hook files,
slapping/slammming code with marked data, and converting data between marks,
including validating data to a mark.  Throughout every computation, `%ford`
keeps track of which resources are dependencies so that the client may be aware
when one or more dependencies are updated.

`%ford` neither accepts unix events nor produces effects.  It exists entirely
for the benefit of applications and other vanes, in particular `%gall`.  `%eyre`
exposes the functional publishing aspects of `%ford` while gall uses `%ford` to
control the execution of applications.  `%clay` is intended to use `%ford` to
managed marked data, but this is not yet reality.
