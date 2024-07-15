# Automate Project Environments with Devbox and Direnv

[Source](https://www.jetify.com/blog/automated-dev-envs-with-devbox-and-direnv/)

## Install Devbox

```bash
curl -fsSL https://get.jetify.com/devbox | bash
```

## Install Direnv

Via Homebrew:

```bash
brew install direnv
```

or [shell](https://direnv.net/docs/installation.html#from-binary-builds):

```bash
curl -sfL https://direnv.net/install.sh | bash
chmod +x direnv
```

Put in in your `$PATH`

## Use

1. In a project directory (or empty dir) run `devbox init`
1. Add dependencies to Devbox. For example, `devbox add nodejs yarn`
1. Add Direnv integration `devbox generate direnv`

To load environment variables from an .`env file`, adjust `.envrc` with `--env-file <name of file>`:

```bash
# Automatically sets up your devbox environment whenever you cd into this
# directory via our direnv integration:

eval "$(devbox generate direnv --print-envrc --env-file .env)"

# check out https://www.jetpack.io/devbox/docs/ide_configuration/direnv/
# for more details
```
