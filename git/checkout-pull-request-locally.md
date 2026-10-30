# Checkout Pull Request Locally

I use this trick quite often to fix errors in pull requests/merge requests.

## GitHub

1. Set a variable for the pull request.

   Bash:

   ```bash
   PR=1234
   ```

   Fish:

   ```bash
   set PR 1234
   ```

2. Use `git fetch` and `git checkout` to fetch the remote pull request.

   ```bash
   git fetch origin pull/$PR/head:pr$PR && git checkout pr$PR
   ```

   The above command will create a new branch on your computer (`pr1234`) and switch to that branch.

   Now you can make changes, for example, you can do a `git pull origin main` and resolve merge conflicts.

   Example workflow:

   ```bash
   git pull origin main
   # fix merge conflicts
   git commit -m "Merge PR #$PR"
   # switch to main branch
   git checkout main
   # merge branch and delete from local machine
   git merge pr$PR && git branch -D pr$PR
   # push to main branch on remote repository
   git push
   ```

## GitLab

1. Set a variable for the merge request.

   Bash:

   ```bash
   MR=1234
   ```

   Fish:

   ```bash
   set MR 1234
   ```

2. Use `git fetch` and `git checkout` to fetch the remote merge request.

   ```bash
   git fetch origin merge-requests/$MR/head:mr$MR && git checkout mr$MR
   ```

   The above command will create a new branch on your computer (`mr1234`) and switch to that branch.

   Now you can make changes, for example, you can do a `git pull origin main` and resolve merge conflicts.

   Example workflow:

   ```bash
   git pull origin main
   # fix merge conflicts
   git commit -m "Merge MR #$MR"
   # switch to main branch
   git checkout main
   # merge branch and delete from local machine
   git merge mr$MR && git branch -D mr$MR
   # push to main branch on remote repository
   git push
   ```

## Worktrees

Same trick works with `git worktree`. You test the PR in a separate directory without switching your current working tree off its branch.

### GitHub

1. Set a variable for the pull request.

   Bash:

   ```bash
   PR=1234
   ```

   Fish:

   ```bash
   set PR 1234
   ```

2. Fetch the remote pull request and create a worktree for it.

   ```bash
   git fetch origin pull/$PR/head:pr$PR && git worktree add ../myrepo-pr$PR pr$PR
   ```

   The first part creates a local branch (`pr1234`); the second checks it out into a new directory next to your repo (`../myrepo-pr1234`).

3. Clean up when done.

   ```bash
   git worktree remove ../myrepo-pr$PR && git branch -D pr$PR
   ```

### GitLab

Same, with the merge request ref:

```bash
MR=1234
git fetch origin merge-requests/$MR/head:mr$MR && git worktree add ../myrepo-mr$MR mr$MR
git worktree remove ../myrepo-mr$MR && git branch -D mr$MR
```

### Detached mode

If you don't want to keep a local branch:

```bash
git fetch origin pull/1234/head
git worktree add --detach ../myrepo-pr1234 FETCH_HEAD
```

Commit before removing the worktree or note the SHA. Otherwise the commit is unreachable once the worktree is gone.

### Merging the worktree

From your main repo directory, where `master` is checked out:

```bash
git merge pr$PR
git push
git worktree remove ../myrepo-pr$PR
git branch -D pr$PR
```

If there are conflicts, resolve them inside the worktree first:

```bash
cd ../myrepo-pr$PR
git merge master        # fix conflicts, commit
cd - && git merge pr$PR
```

A branch can't be checked out in two worktrees at once. If another worktree has `master` checked out, do the merge in that directory instead.

### Caveats

- A branch can't be checked out in two worktrees at once, so each PR gets its own `pr$PR` branch.
