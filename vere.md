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

---

##`-M`

---

##`-n`

---

##`-p`

Specify the ames udp listening port.

`bin/vere -p 42665`

It can sometimes help if you get a port pointed at you and run vere with `-p` to specify the ames udp listening port. VMs and docker containers and the like tend to put up some pretty effective barriers to NAT hole punching.

---

##`-r`

---

##`-F`

Fake. Routes all networking over `0.0.0.0` and doesn't check any (carrier) keys. This allows you to start any carrier.

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
it's probably because of ASLR (some shared library got its data mapped in the middle of your address space and you are screwed).  if so, applying ```bash
setarch `uname -m` -R ./bin/vere```
is supposed to help
