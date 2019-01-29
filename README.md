# gitsh

A customized bash shell for working closely with git

The `gitsh` command starts an interactive bash shell tweaked for heavy git
interaction:

  * All git commands available at top-level
    (`checkout master` = `git checkout master`)
  * All git aliases defined in the `[alias]` section
    of `~/.gitconfig` available at top-level.
  * Custom prompt with current branch, repository, and
    work tree dirty indicator.
  * Customizable via `~/.gitshrc` config files;
    for creating aliases, changing the prompt, etc.
  * Runs on top of normal bash (`~/.bashrc`) and
    readline (`~/.inputrc`) configurations.

## Basic Usage

Typical usage is to change into a git working copy and then start the shell:

    $ cd mygreatrepo
    $ gitsh
    ▹ help

Core git commands and git command aliases defined in `~/.gitconfig` can be
used as top-level commands:

    ▹ checkout -b new
    ▹ log -p
    ▹ rebase -i HEAD~10

It's really just a normal bash shell, though, so all commands on `PATH` and any
aliases defined in `~/.bashrc` are also available:

    ▹ ls -l
    ▹ vim somefile

_IMPORTANT: `rm`, `mv`, and `diff` are aliased to their git counterparts. To use
system versions, run `command(1)` (e.g., `command rm`) or qualify the command
(e.g. `/bin/rm`)._

## Prompt

The default prompt shows username, hostname, SSH status, then the relative path
to the current working directory from the root of the work tree, then the branch
name, as well as status indicators.

The gitsh prompt includes ANSI colors when the git `color.ui` option is
enabled. To enable gitsh's prompt colors explicitly, set the `color.sh` config
value to `auto`:

    $ git config --global color.sh auto

Customize prompt colors by setting the `color.sh.branch`, `color.sh.workdir`,
and `color.sh.dirty` git config values:

    $ git config --global color.sh.branch 'yellow reverse'
    $ git config --global color.sh.workdir 'blue bold'
    $ git config --global color.sh.dirty 'red'
    $ git config --global color.sh.dirty-stash 'red'
    $ git config --global color.sh.repo-state 'red'

See [colors in git](http://scie.nti.st/2007/5/2/colors-in-git) for information.

## Customizing

Most `gitsh` behavior can be configured by editing the user or system gitconfig
files (`~/.gitconfig`) either by hand or using `git-config(1)`. The `[alias]`
section is used to create basic command aliases.

The `~/.bashrc` file is sourced before `~/.gitshrc`. Any bash customizations
defined there and not explicitly overridden by `gitsh` are also available.

## License

Copyright 2018-2019 [Jade Michael Thornton](https://jmthornton.net)

Copyright 2008 [Ryan Tomayko](http://tomayko.com/) and [Aristotle
Pagaltzis](http://plasmasturm.org/)

This program is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License, version 2, as published by the Free
Software Foundation.
