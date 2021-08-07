## Repeat a Command x times

The Fish Shell has a [for loop](https://fishshell.com/docs/current/cmds/for.html) construct you can use.

Example:

```sh
for i in foo bar baz; echo $i; end

# would output:
foo
bar
baz
```

If you want to repeat a command, you can use the [GNU `seq` util](https://www.gnu.org/software/coreutils/manual/html_node/seq-invocation.html):

```sh
for i in (seq 5); echo $i; end

# would output:
1
2
3
4
5
```
