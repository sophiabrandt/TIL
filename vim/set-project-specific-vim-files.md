# Set Project Specific .vimrc Files

You can specify and load project-specific `.vimrc` files.

1. Create a `.vimrc/.nvimrc/.exrc` in the root folder of the project.

I chose `.exrc` as it both works for Vim and NeoVim.

2. Enable loading from files in default configuration

In your standard `~/.vimrc`:

```
# execute Ex commands from files and/or environment variables
set exrc
# prevent `:autocmd` shell and write commands from being run inside
# `.vimrc` in current directory
set secure
```
