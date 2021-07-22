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
	git commit -m "Merge PR $PR"
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
	git fetch origin merge-requests/$MR/head:mr$MR && git checkout mr$PR
	```

	The above command will create a new branch on your computer (`mr1234`) and switch to that branch.

	Now you can make changes, for example, you can do a `git pull origin main` and resolve merge conflicts.

	Example workflow:
	```bash
	git pull origin main
	# fix merge conflicts
	git commit -m "Merge MR $MR"
	# switch to main branch
	git checkout main
	# merge branch and delete from local machine
	git merge pr$PR && git branch -D mr$MR
	# push to main branch on remote repository
	git push
	```
