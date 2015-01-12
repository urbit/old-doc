urbit
===
is a general-purpose computing stack designed to live in the cloud.

- `vere` is our virtual machine, written in C that runs urbit.
- [`nock`](doc/nock) is our assembly language. Everything in urbit reduces to `nock`.
- [`hoon`](doc/hoon) is our programming language. `hoon` is strict, typed and functional. 
- [`arvo`](doc/arvo) is our operating system. 

`arvo` is event driven and modular. `arvo` modules are called 'vanes'.

+ [`%ames`](doc/arvo/ames) is our networking protocol.
+ [`%clay`](doc/arvo/clay) is our global, version controlled filesystem. 
+ [`%dill`](doc/arvo/dill) is our terminal.
+ [`%eyre`](doc/arvo/eyre) is our webserver.
+ [`%ford`](doc/arvo/ford) is our functional publishing and asset compilation engine.
+ [`%gall`](doc/arvo/gall) is our application model and storage engine.
+ [`%time`](doc/arvo/time) manages timer events.
+ [`%zuse`](doc/arvo/zuse) is our standard library

---

If you're new to the system, take a look at some of the [guides](doc/guides) to get oriented. Come join us on `:chat` to ask questions and get help. 