# Diff the Delta

[Find out which files were changed](https://stackoverflow.com/questions/7686582/finding-most-changed-files-in-git):

```bash
git log --pretty=format: --since="1 year ago" --name-only -- "*.java" | sort | uniq -c | sort -rg | head -10
```

[Show the history of a file](https://stackoverflow.com/questions/278192/view-the-change-history-of-a-file-using-git-versioning):

```bash
git log --follow -p -- <path-to-file>
```

[Show what a commit did](https://stackoverflow.com/questions/1157818/how-can-i-show-what-a-commit-did):

```bash
git show <commit> -- <name of file>
```
