# Add a comma at each entry and join lines

```bash
:%s/$/,/ | 1,$j
```

- `:%s/$/,/` substitutes (replaces) the end of each line ($) in the file (% specifies the range for the entire file) with a comma (,)
- `1,$j` joins all lines in the file from the first line (1) to the last line ($) into a single line
