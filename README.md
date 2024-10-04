# Documentation for https://github.com/lsculv/dotfiles

This _must_ be a completely separate repo as the `dotfiles` repo needs to match
_exactly_ the structure of the files that live in `$HOME`. If this README or
other docs were added there, it would clutter your home directory whenever you
used it, and complain if you deleted them and tried to add some more files.
A separate docs repo is the best solution for simplicity of installation and use.

## Setup

Use the following commands to install the dotfiles onto a new machine. This will
create a backup of the files that needed to be overwritten when checking out
from the `dotfiles` repo. This will almost always happen due to `.bashrc` being
included, among others.
```bash
alias config='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
git clone --bare https://github.com/lsculv/dotfiles $HOME/.dotfiles
config checkout || \
    config checkout 2>&1 | grep -E "^\s+" | awk '{print $1}' | \
    xargs -I{} /bin/sh -c 'mkdir -p config-backup/"$(dirname {})"; mv {} config-backup/{}'
config checkout
config config --local status.showUntrackedFiles no
```

After this setup it is probably a good idea to reboot, or at least restart any
programs that are effected by these config changes.

