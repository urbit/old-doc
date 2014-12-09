Install
-------------------

###1. Dependencies

Urbit depends on:

    gcc
    gmp
    libsigsegv
    openssl
    automake
    autoconf
    ragel
    cmake
    re2c
    libtool
    libssl-dev (Linux only)
    ncurses (Linux only)

####Ubuntu or Debian

    sudo apt-get install libgmp3-dev libsigsegv-dev openssl libssl-dev libncurses5-dev git make exuberant-ctags automake autoconf libtool g++ ragel cmake re2c

####Fedora

    sudo yum install gcc gcc-c++ git gmp-devel openssl-devel openssl ncurses-devel libsigsegv-devel ctags automake autoconf libtool cmake re2c

####AWS

    sudo yum --enablerepo epel install gcc git gmp-devel openssl-devel ncurses-devel libsigsegv-devel ctags automake autoconf libtool cmake re2c

####OS X

Do you have XCode? Type `gcc` at your terminal prompt.

If it says `no input files`, you have XCode.

Otherwise, install XCode: `https://developer.apple.com/xcode/`, with the command line tools.

To install dependencies pick either one of Homebrew or Macports, but not both:  
  Homebrew -  
  `brew install git gmp libsigsegv openssl libtool autoconf automake`  

  Macports -  
  `sudo port install git gmp libsigsegv openssl autoconf automake`

Although automake/autoconf/libtool are generally installed by default, some
have reported needing to uninstall and reinstall those three packages, at least
with Homebrew.  YMMV.


###2. Build

Clone this repo:

    git clone git://github.com/urbit/urbit.git

`cd` to the unpacked Urbit directory you just created:

    cd urbit

If this works, `ls urb/` should show:

    urbit.pill  zod/

Then just run `make` in the urbit directory.

Sometimes things are just easy.


###3. Run

Run `bin/vere -c mypier` in the urbit directory, where `mypier` is a directory that doesn't yet exist. All your state (an append-only log and a memory checkpoint) will live in this directory.  The name of your pier doesn't matter and is not visible internally.

A _pier_ is an Urbit virtual machine that hosts one or more Urbit identities,
or _ships_.  When you run `bin/vere -c`, it automatically creates a 128-bit ship, or `submarine`.  Your name (a hash of a randomly-generated public key) will look something like:

    ~machec-binnev-dordeb-sogduc--dosmul-sarrum-faplec-nidted

First you'll see a string of messages like:

    vere: urbit home is /Users/cyarvin/Documents/src/u3/urb
    loom: mapped 1024MB
    time: ~2013.9.1..03.57.11..4935
    ames: on localhost, UDP 63908.
    generating 2048-bit RSA pair...

and then it'll pause a little, 'cause this is slow, and then

    saving passcode in /Users/cyarvin/.urbit/~magsut-hopful.txt
    (for real security, write it down and delete the file...)

and, then, if the network gods are happy, your submarine will start pulling
down Arvo files:

     + /~machec-binnev-dordeb-sogduc--dosmul-sarrum-faplec-nidted/main/1/bin/ticket/hoon
     + /~machec-binnev-dordeb-sogduc--dosmul-sarrum-faplec-nidted/main/1/bin/reset/hoon
     + /~machec-binnev-dordeb-sogduc--dosmul-sarrum-faplec-nidted/main/1/bin/ye/hoon
     + /~machec-binnev-dordeb-sogduc--dosmul-sarrum-faplec-nidted/main/1/bin/ls/hoon

and the like.  You'll see a couple pages of this stuff.  Don't worry too much
about the details right now.  Finally, you'll get the Arvo shell prompt (which
is also a Hoon REPL):

    ~machec-binnev-dordeb-sogduc--dosmul-sarrum-faplec-nidted/try=>

If you would like to safely bring this ship back into port (End the Unix process),
just enter Control-D.  

To re-launch your pier after creation run `bin/vere mypier` (exclude the `-c`)

###4. Registration

Arvo instances in the Urbit network, called "ships", are addresses in a finite namespace much like IP numbers.  You should be able to remember your personal IP number. However, numbers are cumbersome for humans to memorize.  Urbit solves this problem by mapping each address to a phonetic name, whose length is proportional to how many of that type of ship there are.  

In this section, we'll get you registered with some Urbit ships. One of these ships, a destroyer, will be both your personal cloud computer and identity in the social network of Urbit.

The long name in your prompt now is that of a submarine. Submarines are  cheap, temporary ships that are tiring to remember but useful for trying Urbit out or browsing anonymously. But this moniker is mouthful.  You can stick with it for now, but you're going to need a wider xterm.

Instead, registering for a destroyer will get you a nice short name like

    ~waclux-tomwyc

Destroyers are rarer ships meant to be associated with a user's digital identity. They are far fewer destroyers in the Urbit namespace than submarines. 

[During this period of development we are no longer giving away destroyers. If you would like to know when we are offering ships again, please head to urbit.org and enter your email address or email ship [at] urbit.org]

Your destroyers will arrive in the form of `[ship ticket]` pairs.
Let's say one of your ships is `~waclux-tomwyc` and its ticket is

    ~ribdyr-famtem-larrun-figtyd

(Where do we get these phonetic strings from, anyway?  Just random unsigned integers,
rendered in Hoon's syllabic base, `@p`.)

A new life awaits you on the off-world colonies!  To begin, just
type at the submarine prompt:

    :begin ~waclux-tomwyc

and follow the directions.  When the script completes, hit return
and you'll be the `~waclux-tomwyc` you wanted to be.  

###Chat

To start chatting, simply type

    ~waclux-tomwyc/try=> :chat

and type `?` for the list of commands once `:chat` is running. 

Most of us are hanging out on `:chat` regularly. We can answer any questions you might have and help you get oriented in this new environment.