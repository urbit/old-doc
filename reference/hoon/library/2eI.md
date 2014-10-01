section 2eI, parsing (external)       

###++rash

```
++  rash  |*([naf=@ sab=_rule] (scan (trip naf) sab))   ::
```
        
Parse a cord with a given rule and crash if the cord isn't entirely parsed.

####Examples

        ~tadbyl-hilbel/try=> (rash 'I was the world in which I walked, and what I saw' (star (shim 0 200)))
        "I was the world in which I walked, and what I saw"
        ~tadbyl-hilbel/try=> (rash 'abc' (just 'a'))
        ! {1 2}
        ! 'syntax-error'
        ! exit
        ~tadbyl-hilbel/try=> (rash 'abc' (jest 'abc'))
        'abc'
        `~tadbyl-hilbel/try=> (rash 'abc' (jest 'ab'))
        ! {1 3}
        ! 'syntax-error'
        ! exit

###++rush

```
++  rush  |*([naf=@ sab=_rule] (rust (trip naf) sab))
```

Parse a given with a given rule and produce null if the cord isn't entirely parsed.

####Examples

        ~tadbyl-hilbel/try=> (rush 'I was the world in which I walked, and what I saw' (star (shim 0 200)))
        [~ "I was the world in which I walked, and what I saw"]
        ~tadbyl-hilbel/try=> (rush 'abc' (just 'a'))
        ~
        ~tadbyl-hilbel/try=> (rush 'abc' (jest 'abc'))
        [~ 'abc']
        ~tadbyl-hilbel/try=> (rush 'abc' (jest 'ac'))
        ~
        ~tadbyl-hilbel/try=> (rush 'abc' (jest 'ab'))
        ~

###++rust

```
++  rust  |*  [los=tape sab=_rule]
          =+  vex=((full sab) [[1 1] los])
          ?~(q.vex ~ [~ u=p.u.q.vex])
```

Parse a tape with a given rule and produce null if the tape isn't entirely parsed.

####Examples

        ~tadbyl-hilbel/try=> (rust "I was the world in which I walked, and what I saw" (star (shim 0 200)))
        [~ "I was the world in which I walked, and what I saw"]
        ~tadbyl-hilbel/try=> (rust "Or heard or felt came not but from myself;" (star (shim 0 200)))
        [~ "Or heard or felt came not but from myself;"]
        ~tadbyl-hilbel/try=> (rust "And there I found myself more truly and more strange." (jest 'And there I'))
        ~

++  scan

Parse a tape with a given rule and crash if the tape isn't entirely parsed.

####Examples

        ~tadbyl-hilbel/try=> (scan "I was the world in which I walked, and what I saw" (star (shim 0 200)))
        "I was the world in which I walked, and what I saw"
        ~tadbyl-hilbel/try=> (scan "Or heard or felt came not but from myself;" (star (shim 0 200)))
        "Or heard or felt came not but from myself;"
        ~tadbyl-hilbel/try=> (scan "And there I found myself more truly and more strange." (jest 'And there I'))
        ! {1 12}
        ! 'syntax-error'
        ! exit


