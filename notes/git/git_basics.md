# Git basics
Some simple explanations of git basics.

## Workflows
Different workflows for git.

### Commit

```bash
# add file
> git add <filename>
> git add *

# commit changes
> git commit -m "Commit message"
```

### Branch and merge
How to branch for a bug fix/new feature and merge the changes.

```bash
# create branch and switch to it
> git checkout -b branch_name

# commit changes
> ...

# change back to master/dev
> git branch master

# pull latest changes
> git pull (--rebase)

# merge with branch
> git merge branch_name
```

### Rebase
Keep a clean history with rebase.
* `dev` - the main branch
* `feature` - the newly created branch

Always rebase before a merge.

```bash
# checkout new branch
> git checkout -b feature

# make commits
> ...

# make a pull with rebase before merge (if long branch, do occasional rebases)
> git checkout dev
> git pull --rebase
> git checkout feature
> git rebase dev

# merge when done
> git checkout dev
> git merge feature

# delete branch
> git branch -d feature
```
