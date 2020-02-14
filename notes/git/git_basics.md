# Git basics

Some simple explanations of git basics.

-   [Git basics](#git-basics)
    -   [Workflows](#workflows)
        -   [Commit](#commit)
        -   [Branch and merge](#branch-and-merge)
        -   [Rebase](#rebase)
        -   [Squash](#squash)
    -   [Aliases](#aliases)
        -   [Logline](#logline)
        -   [Contributors by merge](#contributors-by-merge)
        -   [Delete local branches](#delete-local-branches)

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

-   `dev` - the main branch
-   `feature` - the newly created branch

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

### Squash

If you need to squash (combine) commits into one, this is how. If you're at your feature branch with a lot of commits, be sure to be at the latest.

```bash
# this will take the 3 latest commits, including the current one.
> git rebase -i HEAD~3
```

Your text editor will open and look something like this. These are the 3 commits we choose.

```bash
pick 7f9d4bf Accessibility fix for frontpage bug
pick 3f8e810 Updated screenreader attributes
pick ec48d74 Added comments & updated README
# ...
```

Replace `pick` with `squash` for those you want to combine. The main one should still have pick.

```bash
pick 7f9d4bf Accessibility fix for frontpage bug
squash 3f8e810 Updated screenreader attributes
squash ec48d74 Added comments & updated README
# ...
```

Save and exit, now it's time to edit the comments.

```bash
# This is a combination of 3 commits
# This is the 1st commit message:

Accessibility fix for frontpage bug

# This is the commit message for #1:

Updated screenreader attributes

# This is the commit message for #2:

Added comments & updated README
# ...
```

Comment out all the commits you don't want to use, and only leave the one you want. Save and exit.

**Done**, now you can merge or rebase.

## Aliases

Some good aliases I have stumbled upon. It is possible to either add by global command or to the `.gitconfig` file. Get the location of the file with the following command (look at the file name):

```bash
git config --global --edit
```

### Logline

Print your git log much better with this alias.

```bash
# create alias
> git config --global alias.logline "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# call alias
> git logline
```

### Contributors by merge

Get all contributors ranked by merge

```bash
# create alias
> git config --global alias.contributors "shortlog -sn --no-merges"

# call alias
> git contributors
```

### Delete local branches

Delete all local branches

```bash
# add to file
deletebranches = !git branch --merged | grep -v '*' | xargs -n 1 git branch -d

# call alias
> git deletebranches
```