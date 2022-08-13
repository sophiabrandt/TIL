# Add a New Line After Pattern

[Source](https://fedingo.com/how-to-add-newline-after-pattern-in-vim/)

```bash
:%s,<pattern>,<pattern>\r,g
```

* search and replace `<pattern>` with the same pattern but adding a return `\r`
