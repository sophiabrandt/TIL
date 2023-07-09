# Use entr to reload commands

Install [entr](https://github.com/eradman/entr#man-page-examples).

Launch and relaunch a Node.js server:

```fish
ls *.js | entr -r node app.js
```

Render markdown file in terminal on change:

```fish
ls README.md | entr -rs 'glow README.md'
```

(entr works in other shells, too.)
