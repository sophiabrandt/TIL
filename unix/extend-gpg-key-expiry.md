# Extend GPG key expiry without knowing the key ID

Find the key ID first:

```sh
gpg --list-keys --keyid-format long
```

Look for the `pub   rsa4096/<KEYID>` line. That long hex string is the key ID.

Interactive:

```
gpg --edit-key <KEYID>
gpg> expire
Date should be: YYYY-MM-DD
gpg> save
```

Run `help` in edit-key mode to list valid commands.

Non-interactive:

```sh
gpg --quick-set-expire <KEYID> 2026-12-31 primary
gpg --quick-set-expire <KEYID> 2026-12-31 sub
```

Omit the number to extend all subkeys. Pass `sub <n>` to extend one.

Notes:

- Works on already-expired keys. The expiry check runs after you set the new date.
- If the listing shows `sec#`, the secret key is missing. Re-import it first. You can't extend a signing key from a public-only copy.
- Narrow the search with `gpg --list-secret-keys` or `gpg --list-keys <email>` when multiple keys match.
