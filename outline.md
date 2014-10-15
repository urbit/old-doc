Setup
  We should write this last. When the docs come out we'll probably have a different setup process than we do now.


Guide

These are very much subject to change as we work through them. In general, these should conform to the convention of: example, how to run it, and how to change parts of it. The intent is to cover concepts at a purely practical level and link to more in-depth explanations.

  Basic hoon using %ford
  Introducing hoon concepts by building a simple blogging system with %ford. 
  Topics:
    ++sail
    Assignment
    runes
    odors
    tiles
    cores
    recursion
    %ford runes

  Basic arvo using the CLI
  Introducing arvo concepts by navigating your ship in the command line
  Topics:
    REPL basics
    %clay
    :cd, :ls, :mv
    Env vars
    :reset, :update, :wipe

  Basic %gall app
  More advanced hoon concepts shown by building a stateful app
  Topics:
    urb.js
    %gall, saving and updating state
    subscriptions, keeping track of subscribers
    %ames, message passing

  Full-featured applications
  An application using both %ford and %gall
  Topics:
      Parsing
      Advanced urb.js
      Writing to %clay

  Nock
    Although there aren't any applications to be built with Nock, it's fun to get a feel for it by example.

Nock
  Overview
    This is basically what's at the top of nock.md.
  Commentary
    This is basically the rest of nock.md

Hoon
  Overview
    Discussion of the hoon language and its high level features. This could continue in more detail on specific topics:
    
    Type / Tiles
      This is separate from the library doc that can be found under ++type and ++tile
    Cores / Gates

  Rune index
    Each category of rune should have an overview section. % runes, ++sail runes, &c.
    
    Our existing rune doc is pretty close. Each rune should have:
    
    Syntax
    An explanation of how the rune is used. What it accepts, what it produces and common usage. This should start with something that looks like: |_, barcab, [%brcb p=tile q=(map term foot)]. [rune], [pronunciation], [model definition]. This should also include whether the rune is a tile or a twig.
    
    Examples
    Both tall and wide form are important. Examples should have short commentary explaining their function. They should be easily paste-able into a file or repl
    
    Definition, Expansion
    Presently these include all of the dependent models and the expansion from ++open (or related). I'm on the fence about how important these are. Would defer to someone else.

  Quick Reference
    Irregular form index
    Odor index
    urb.js
    %eyre access methods
    .^ methods
    hardcoded %gall arms
    Glossary

  Library index
    This should cover all of our library functions in hoon.hoon and zuse.hoon. Similar to our Rune index, discussion topics can be covered as overviews in-line with their topics. Each arm should include the following:

    Source
    Just the source.
    
    Comment
    A <= one sentence comment
    
    Summary
    A paragraph or so covering usage and internals 
    
    Examples
    Preferably that can be pasted in to a repl
  
Arvo

  System overview
    This should describe the system at a high level. What a vane is, basics of how events work, how the vanes fit together, &c. This should also act as an entry point for learning more about specific topics that live in the individual vane documentation. This could also be the place to document some of our built-in applications, such as :reload or :reset.

  Commentary
    Covering the lower part of hoon.hoon where arvo itself is implemented

  Vanes
    Each vane should have the following as a part of its documentation:

    Overview
    A discussion of the vane for someone simply interested in the system. This should give an idea of how it fits in to the OS as a whole, and how its public methods are used. Ideally these clock in at around 300 - 500 words and provide links to more technical parts of the doc when possible.

    Models
    Should follow a similar style to the reference doc, with examples where they're needed.

    Public interface
    This is probably the most used part of each vane's doc, since developers arrive here when trying to actually use vane methods. Whether examples or clear, concise commentary is more appropriate here I'm not sure.

    Commentary
    Technical commentary on the vane's internals in the spirit of the Lion's Commentary (http://en.wikipedia.org/wiki/Lions'_Commentary_on_UNIX_6th_Edition,_with_Source_Code)

    %ames
      The overview of Ames seems like a logical place for a discussion of the namespace
    %clay
    %dill
    %eyre
    %ford
    %gall
    %ives
    %jael
    %kahn
    %lunt
