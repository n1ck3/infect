infect
======

**infect** is a single file configuration file distribution system.  You use it to
create tarball bundles of your configuration files, deploy them on a web server
and then, on a new uninfected system, use curl as such:

    curl infect.example.com | sh

...and two seconds later your system is now infected with your superb taste in
configuration files!

Options and watnot
------------------

**infect** / **infect update**

Run the script without arguments or with the *update* argument to perform a full
update. That is, download a new tarball, unpack it, and symlink all the files.

**infect symlink**

Use the recipes in the .pkgs files to create symbolic links from the
configuration file root to where the applications actually look for them. If any
of the files exists, they will be moved into the **backup/** directory in the
configuration file root.

**infect deploy [web_dir]**

Create a new tarball snapshot from the current configuration files and move it
to the *[web_dir]* (or `$INFECT_WEB_DIR`). If the variable is unset
`/srv/infect` will be used as a default. If *[web_dir]* looks like
a remote address (such as `user@host:/dir`) rsync will be used to send it there.

**infect mutate [src [dest]]**

Takes all files in *[src]* (or `$INFECT_MUTATE_DIR`) and puts them in
*[dest]* (or `$INFECT_DIR`). Useful when using someone elses configuration files
as a base for your own, and using the mutate dir to inject your own changes.

**infect zsh-completion**

Print the zsh code needed for completion of the infect commands. Use
`$(infect zsh-completion)` in your zshrc and it will set it up for you!

Environment variables
---------------------

`$INFECT_DIR` [$HOME/etc]

`$INFECT_WEB_DIR` [/srv/infect]

`$INFECT_MUTATE_DIR` [$HOME/local]

License
-------

Copyright (c) Lowe Thiderman.  Distributed under the BSD license.
