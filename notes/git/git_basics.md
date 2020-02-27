# Git basics

-   [Git basics](#git-basics)
    -   [Commit](#commit)
    -   [Branch and merge](#branch-and-merge)
    -   [Rebase](#rebase)
    -   [Squash](#squash)
        -   [Squash latest commits](#squash-latest-commits)
        -   [Squash earlier commits](#squash-earlier-commits)
    -   [Aliases](#aliases)
        -   [Logline](#logline)
        -   [Contributors by merge](#contributors-by-merge)
        -   [Delete local branches](#delete-local-branches)

## Commit

```bash
# add file
> git add <filename>
> git add *

# commit changes
> git commit -m "Commit message"
```

## Branch and merge

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

## Delete branch

### Deleting local branches

```bash
> git branch -d feature/login
```

_Note: you might want to use the `-f` flag if you have unmerged changes._

### Deleting remove branches

```bash
> git push origin --delete feature/login
```

## Rebase

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

## Squash

### Squash latest commits

If you need to squash (combine) commits into one, this is how. If you're at your feature branch with a lot of commits, be sure to be at the latest.

**This is the commit history**

![](https://i.imgur.com/wKWEyCX.png)

We only want to include the 3 latest commits, including the current one.

![](https://i.imgur.com/zUCAiaa.png)

```bash
# this will take the 3 latest commits, including the current one.
> git rebase -i HEAD~3

# you can also use the commit hash before the one you want to use
> git rebase -i b1e1d4f
```

If you choose to use the commit hash, for example, these three will be included if you use the hash with the arrow.

![](https://i.imgur.com/DqvFeEs.png)

Your text editor will open and look something like this. These are the 3 commits we choose.

![](https://i.imgur.com/fSAM0yu.png)

Replace `pick` with `squash` (or `s`) for those you want to combine. The main one should still have pick. Save and exit.

![](https://i.imgur.com/hy2BzM0.png)

Now, a window with all commit messages will pop up.

![](https://i.imgur.com/qGXJ8cC.png)

Comment out the commit messages of the commits you want to squash and edit the message of the one you want to persist.

![](https://i.imgur.com/H6p4qTg.png)

Comment out all the commits you don't want to use, and only leave the one you want. Save and exit.

**Done**, now you can merge or rebase.

This is what the commit history looks like now:

![](https://i.imgur.com/iJ5eb1y.png)

### Squash earlier commits

If you want to only squash earlier messages, like this:

![](https://i.imgur.com/sOSspZf.png)

Do a interactive rebase on at least 2 commits before, `1 - removed all files`.

```bash
> git rebase -i <hash-commit>
```

Use either `s` or `f` to the commits (or `squash` or `fixup`).

-   `squash` - modify commit message
-   `fixup` - remove commit message

![](https://i.imgur.com/ibO0bLx.png)

The two commits that should be changes is now added. Save and go to next file.

![](https://i.imgur.com/2fP5Eyh.png)

Comment out the two commit messages that you want to change and rewrite the earlier commit (earlier named `2 - added one file and squashed`), now named whatever you want.

Save and the two files will now be squashed with the earlier commit. This is how it looks now:

![](https://i.imgur.com/84Ui2G7.png)

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