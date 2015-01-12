Vere is the Urbit virtual machine. 

        bin/vere -c ship

#Options

##`-c`

Create. Creates a new pier. Takes a folder name, such as `pier`.

`bin/vere -c pier`

---

##`-k`

---

##`-L`

Looks for all the carriers at localhost instead of at *.urbit.org

`bin/vere -L`

---

##`-M`

---

##`-n`

---

##`-p`

Specify the [ames](doc/arvo/ames) udp listening port.

`bin/vere -p 42665`

It can sometimes help if you get a port pointed at you and run vere with `-p` to specify the [ames](doc/arvo/ames) udp listening port. VMs and [docker](http://www.docker.com/) containers and the like tend to put up some pretty effective barriers to [NAT](http://en.wikipedia.org/wiki/Network_address_translation) [hole punching](http://en.wikipedia.org/wiki/TCP_hole_punching).

---

##`-r`

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

##`-X`

---

#Tips
##inability to mmap 2Gb with MAP_FIXED:
it's probably because of [ASLR](http://en.wikipedia.org/wiki/Address_space_layout_randomization) (some shared library got its data mapped in the middle of your address space and you are screwed).  if so, applying ```bash
setarch `uname -m` -R ./bin/vere```
is supposed to help
