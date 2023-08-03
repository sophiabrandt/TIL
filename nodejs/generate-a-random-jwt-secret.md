# Generate a random JWT secret

```bash
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))" | pbcopy
```

[Source](https://stackoverflow.com/a/70986164)
