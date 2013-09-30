easy-vcs-status for zsh
=======================

Synopsis
--------

* easy-vcs-status - a zle tweak for easy access to VCS status

Description
-----------

![Screen shot](../master/screenshot1.png?raw=true)

This tweak allows user to see VCS status in the completion menu UI
when the tab key is hit when the command line is empty.

VCS status is shown in the completion menu which is scrollable back
and forth.  If you hit enter to finish the completion, the full output
is written to the standard output.  Otherwise, the menu simply
disappears and user can get back to normal operation on the command
line.

How to set up
-------------

A variable defined by `vcs_info` is used to figure out what VCS is
used in the current directory, so `vcs_info` must be loaded and
configured in order for this tweak to work.

Given `vcs_info` is set up, put the file `easy-vcs-status` somewhere
in your `$fpath` and add these lines to your `.zshrc`:

    autoload -Uz easy-vcs-status
    easy-vcs-status

This binds the tab key to `expand-or-complete-or-vcs-status`, a
wrapper of `expand-or-complete` that casts all the magic.

Configuration
-------------

Commands for showing VCS statuses are configurable via `zstyle` as
follows:

    zstyle ":easy-vcs-status:${vcs}" command "${command}"

For convenient scrolling through a long status output, I strongly
suggest binding keys in the menuselect keymap if you haven't, for
example:

    zmodload zsh/complist
    bindkey -M menuselect '\e[Z' reverse-menu-complete
    bindkey -M menuselect '^V' forward-word
    bindkey -M menuselect '^[v' backward-word
    bindkey -M menuselect '^[<' beginning-of-history
    bindkey -M menuselect '^[>' end-of-history

License
-------

Copyright (c) 2013 Akinori MUSHA

Licensed under the 2-clause BSD license.
See `LICENSE` for details.
