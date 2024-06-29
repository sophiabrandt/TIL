# How to set multiple workspaces (GOPATH)

> A Go Workspace is how Go manages our source files, compiled binaries, and cached objects used for faster compilation later. It is typical, and also advised, to have only one Go Workspace, though it is possible to have multiple spaces. The `GOPATH` acts as the root folder of a workspace. [^1]

## Why multiple workspaces?

I'd like to install my global binaries into a central location. These programs are third-party CLIs that I want to use everywhere in my terminal as a consumer. I don't develop these progams.

At the same time, I'd like to make sure that my `GOPATH` is correct for my actual projects that I'm working on.

> Executables are installed in the directory named by the GOBIN environment variable, which defaults to $GOPATH/bin or $HOME/go/bin if the GOPATH environment variable is not set. [^2]

## How to Set GOPATH?

Check the [wiki][wiki] for your operating system and shell.

For Unix, Fish shell:

```sh
set -x -U GOPATH $HOME/.go:$HOME/projects/go/workspace
```

This command sets an universal variable for both `$HOME/.go` and `$HOME/projects/go/workspace`.

## Fish Shell: Add GOPATH folders to $fish_user_paths

[Use `fish_add_path` to add more locations to fish's `$PATH`.](https://fishshell.com/docs/current/cmds/fish_add_path.html)

To use the "global" Go binaries as well as your own workspace binaries:

```sh
fish_add_path $HOME/.go
fish_add_path $HOME/projects/go/workspace
```

[^1]: [Understanding the GOPATH][do]

[^2]: [golang.org](https://golang.org/cmd/go/#hdr-Compile_and_install_packages_and_dependencies)

[do]: https://www.digitalocean.com/community/tutorials/understanding-the-gopath
[wiki]: https://github.com/golang/go/wiki/SettingGOPATH
