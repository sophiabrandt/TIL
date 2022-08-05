# Remove from PATH

```bash
echo $PATH | tr ":" "\n" | grep -v '/usr/local/bin' | xargs | tr ' ' ':'
```

Also works with fish shell using [replay](https://github.com/jorgebucaran/replay.fish).

Source: [Unix Stackexchange](https://unix.stackexchange.com/questions/108873/removing-a-directory-from-path)
