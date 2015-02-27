easy-vcs-status for zsh
=======================

Synopsis
--------

* easy-vcs-status - a zle tweak for easy access to VCS status

Description
-----------

![Screen shot](../master/screenshot1.png?raw=true)

This tweak allows user to pop up VCS status using the completion menu
UI with a key combination (default: `Meta-Shift-S`) whenever you are
on the command line.

VCS status is shown in the completion menu which is scrollable back
and forth.  If you hit enter, the full output is written to the
standard output.  If you hit space, the last shell word on the current
line is pasted into the previous command line as result of the
completion.  Otherwise, the menu simply disappears and user can get
back to normal operation on the command line with the previous input.

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

Keys for opening and closing VCS status popups are configurable via
`zstyle` as follows:

    # Use Meta-Control-S instead
    zstyle ":easy-vcs-status:bindkey" open '^[^S'

You can alternatively manually bind a key to the function
`open-vcs-status`.

Commands for showing VCS statuses are configurable via `zstyle` as
follows:

    zstyle ":easy-vcs-status:command" "$vcs" "$command"

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

Copyright (c) 2013-2015 Akinori MUSHA

Licensed under the 2-clause BSD license.
See `LICENSE.txt` for details.
