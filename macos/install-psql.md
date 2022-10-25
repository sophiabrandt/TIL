# Install psql via Homebrew on MacOS

Installations for Fish shell (M1):

```fish
brew install libpq
```

Add to path:

```fish
fish_add_path /opt/homebrew/opt/libpq/bin
```

```bash
echo 'echo export PATH="/opt/homebrew/opt/libpq/bin:$PATH"' >> ~/.bashrc
```

Source: [StackOverflow](https://stackoverflow.com/questions/44654216/correct-way-to-install-psql-without-full-postgres-on-macos)
