Vere is the Urbit virtual machine. 

        bin/vere -c ship

#Options

##`-b`

batch create

---

##`-c`

Create. Creates a new pier. Takes a folder name, such as `pier`.

`bin/vere -c pier`

---

##`-d`

daemon

---

##`-D`

dry compute

dry compute the north and/or south events

---

##`-f`

fuzz testing

---

##`-k`

kernel version

---

##`-l`

raft port

---

##`-L`

Localhost. Routes all networking over `0.0.0.0` and checks the keys.

`bin/vere -L -I ~del -c fz`

---

##`-M`

memory madness

---

##`-n`

unix hostname

---

##`-p`

Specify the [ames](doc/arvo/ames) udp listening port.

`bin/vere -p 42665`

It can sometimes help if you get a port pointed at you and run vere with `-p` to specify the [ames](doc/arvo/ames) udp listening port. VMs and [docker](http://www.docker.com/) containers and the like tend to put up some pretty effective barriers to [NAT](http://en.wikipedia.org/wiki/Network_address_translation) [hole punching](http://en.wikipedia.org/wiki/TCP_hole_punching).

---

##`-P`

profile

---

##`-q`

quite (see also [`:verb`](reference/arvo/util.md#verb)). (inverse of [`-v`](#-v))

---

##`-r`

raft flotilla

needs also the [`-l`](#-l) option set

---

##`-F`

Fake. Routes all networking over `0.0.0.0` and doesn't check any keys. This allows you to start any carrier.

`bin/vere -F -I ~zod -c zod`

You get an isolated network with just yourself but you can [`:ticket`]() other ships or start other ships or start other carriers.

---

##`-I`

Imperial. Takes a carrier name, such as `~zod`.

`bin/vere -F -I ~zod -c zod`

---

##`-v`

verbose (see also [`:verb`](reference/arvo/util.md#verb)). (inverse of [`-q`](#-q))

`bin/vere -v mypier`

---

##`-X`

skip last event

`bin/vere -Xwtf mypier`

---

#Tips
##inability to mmap 2Gb with MAP_FIXED:
it's probably because of [ASLR](http://en.wikipedia.org/wiki/Address_space_layout_randomization) (some shared library got its data mapped in the middle of your address space and you are screwed).  if so, applying ```bash
setarch `uname -m` -R ./bin/vere```
is supposed to help
