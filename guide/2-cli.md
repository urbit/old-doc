This guide is intended to get you oriented in the Arvo command prompt and give you a tour of some basic utilities. The command prompt comes in two flavors, in a web browser and in a terminal. For the most part they're the same, except that in a browser you can evaluate tall-form Hoon expressions but you can't run readline apps, such as `:chat`.

This rudimentary tour should work well in both places. 


1

Move around `%clay`

After finishing the [setup instructions]() you should have an Arvo prompt that looks like this:

    ~talsur-todres/try=>

The path at the beginning of your prompt is actually a path in the global filesystem of Urbit, called `%clay`. Since `%clay` is universal across all of Urbit, each full path starts with a ship name. `%clay` is also versioned on a per-desk basis. Desks are the top-level directories in your pier.

Moving around `%clay` is simple. There is no equivalent of `cd`. Instead, just type a valid path name at the prompt to move to that directory. Here we'll move to our starting root path in the try desk, `/try=` to the `main` desk:

    ~talsur-todres/try=> /=main=
    =% /~talsur-todres/main/0
    ~talsur-todres/main=> 

We have two shortcuts in `%clay` that are worth noting, `=` and `%`. 

`=` copies in some corresponding part of our current path. In the second line above you can see how the `=` in `/=main=` pull in the `~talsur-todres` and `0` in from our starting directory, `/~talsur-todres/try/0`. It's important to note that our full prompt to start is `/~talsur-todres/try=`, where the trailing `=` indicates the current revision. In the shell, revision `0` never exists — it's used as a pointer to the head.

`%` is similar to `.` in unix: 

    ~talsur-todres/main=> %
    =% /~talsur-todres/main/0
    ~talsur-todres/main=> %%
    [~.~talsur-todres ~.main ~]
    ~talsur-todres/main=> %%%
    [~.~talsur-todres ~]
    ~talsur-todres/main=> %%%%
    ~

When using `%` to move around in `%clay` you need to make sure to use leading and trailing `/` to ensure your path is interpolted correctly:

    ~talsur-todres/main=> /%%%/try=
    =% /~talsur-todres/try/0
    ~talsur-todres/try=> 


2

Create some revisions

Let's use `:into`, our simple utility for writing text to a file, to create a new file:

    ~talsur-todres/try=> :into %/helo/txt 'helo mars'
    written
    ~talsur-todres/try=> 

To confirm that our file was written, we can use `:ls`. `:ls` prints a list of directory contents, but requires that you specify a path. `%` will suffice for the current path:

    ~talsur-todres/try=> :ls %
    readme helo
    ~talsur-todres/try=> 

Let's update our file with some new content, so we can see how `%clay` stores revisions.

    ~talsur-todres/try=> :into %/helo/txt 'gbye mars'
    written
    ~talsur-todres/try=> :ls /=try/1
    readme helo
    ~talsur-todres/try=> :cat /=try/1/helo/txt
    /~talsur-todres/try/9/helo/txt
    helo mars
    ~talsur-todres/try=> :cat /=try/2/helo/txt
    /~talsur-todres/try/10/helo/txt
    gbye mars
    ~talsur-todres/try=> :cat /=try=/helo/txt
    /~talsur-todres/try/~2014.11.26..01.06.33..c93a/helo/txt
    gbye mars
    ~talsur-todres/try=> 

Here we use `:ls` to investigate the filesystem across versions. You can see that our `helo` file exists in our first revision. Using the simple `:cat` command we can print the contents of `/=try/helo/txt` in its two separate, versioned states.


3

Start a yacht

Each Urbit destroyer can delegate around four billion yachts. Yachts are also urbit ships, but are pegged to their parent identity, and are set up to mirror their filesystem. We can generate a `[ship: ticket]` pair for a yacht by using the `:ticket` utility:

    ~talsur-todres/try=> :ticket ~talsur-todres-talsur-todres
    ~talsur-todres-talsur-todres: ~figpem-fapmyl-wacsud-racwyd

Every yacht for a particular destroyer ends in the same `ship-name`, and has every possible destroyer prefix. For example, `~tasfyn-partyv-talsur-todres` is also a valid yacht from `~talsur-todres`.

Start up a new `vere` process with something like `bin/vere -c yacht`. Then run `:begin` and enter the `[ship: ticket]` pair you just generated when prompted. When the process is complete you should get a `; ~talsur-todres-talsur-todres :y1: is your neighbor` message on your destroyer. To confirm that everything is working properly, you can use `:hi` to send a message:

    ~talsur-todres/try=> :hi ~talsur-todres-talsur-todres "whats up"
    hi ~talsur-todres-talsur-todres successful
    ~talsur-todres/try=> 

Which will appear on your new yacht:

    < ~talsur-todres: whats up
    ~tasfyn-partyv-talsur-todres/try=> 

