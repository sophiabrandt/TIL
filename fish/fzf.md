# fzf

| Goal | Command |
|------|---------|
| List files (fast, gitignore-aware) | `fd -t f` or `rg --files` |
| Include hidden, keep gitignore | `fd -t f -H` |
| Scope to a subtree | `fd -t f . src/` |
| Pick + preview | `fd -t f \| fzf --preview 'bat --color=always {}'` |
| Open in running nvim | `nvim --server $TMPDIR/nvim.pipe --remote FILE` |
| Open at line | `nvim --server $SOCK --remote +42 FILE` |
| Popup picker | `fzf --popup 90%,70%` (or `tmux display-popup -E`) |
| Multi-file open | `fzf -m --bind 'enter:become(nv {+})'` |
| Fish integration | `fzf --fish \| source` → Ctrl-T, Ctrl-R, Alt-C |
