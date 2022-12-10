# Useful commands

* [Git](#git)
  * [Git config](##git config)
  * [Git audit commands](##git audit commands)
  * [Git developer commands](###git developer commands)
* [Docker](#docker)

## Git

### Git config

#### Clone shortcuts

Modifies the global config of Git aliasing the given URL with the given keyword

```bash
git config --global url."git@github.com:julplee/".insteadOf "julplee:"
```

Use if like this to clone the repository `useful-commands` of julplee's github `git@github.com:julplee/`

```bash
git clone julplee:useful-commands
```

#### Use KDIFF3 as diff tool

From this [StackOverflow link](https://stackoverflow.com/questions/33308482/git-how-configure-kdiff3-as-merge-tool-and-diff-tool). You just need to execute the following commands:

```bash
git config --global merge.tool kdiff3
git config --global mergetool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
git config --global mergetool.kdiff3.trustExitCode false

git config --global diff.guitool kdiff3
git config --global difftool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
git config --global difftool.kdiff3.trustExitCode false
```

### Git audit commands

#### List Remote Git Branches By Author sorted by committerdate:

```bash
git for-each-ref --format='%(committerdate) %09 %(authorname) %09 %(refname)' 

git for-each-ref --format='%(committerdate) %09 %(authorname) %09 %(refname)' | sort -k5n -k2M -k3n -k4n | grep UXP
```

#### List commits of one developer in all branches
```bash
git log --date=short --all --since=2.months.ago --author=sami@team-latech.io
```

#### Save commits of all developers in all branches in a file
```bash
git log --all  --date-order --format='%ai , %an ,<%ae> ,%h , %D ,%f' >> logs.csv
```

### Git developer commands

#### Add partial (or hunks)

`git add -p` (for partial) allows to add part of a modified file. Git will display hunks of the file one by one and ask if you want to add them

```bash
git add -p
```

#### Blame

To discover why and when a certain line was added, Git can annotate each line of a source file with the name and date it came into existence

```bash
git blame <filename>
```

#### Rebase

Rebase allows to integrate changes from a branch onto another. Alternatively, it's really helpful to help rewriting history

```bash
git rebase -i master
```

you can just rewrite history of the branch by doing (or of the last four commits with HEAD~4)

```bash
git rebase -i HEAD~4
```

#### Stash

Git offers a useful feature for those times when file modifications are in an incomplete state and not yet ready for a commit.
To temporarily return to the last commit, yet retain any uncommited changes, using stash on modified files places all uncommitted changes onto a stack.

```bash
git stash
```

When you are ready to write the stashed changes back into the working copy of the files, simply pop them back off the stack.

```bash
git stash pop
```

#### Diff tool

```bash
git difftool <commit1> [<commit2>]
```

#### Diff of staged files

```bash
git diff --staged
```

#### Work easily with a monorepository

When you need to work on several differents things in a monorepo, let's say adding features and fixing bugs that come along you can make use of `git worktree`

```bash
git pull [my-monorepo]
git worktree add ../devel-new-feature
git worktree add ../fix-this-bug
```

The different worktrees are in sync with the master (the first directory pulled) so you just have to pull the master to sync the others with `git rebase master`

To list all worktrees: `git worktree list`
To delete a worktree: `git worktree prune` after deleting folder
To create a worktree from an existing commit: `git worktree add [worktree-path-and-name] [commit-hash-or-tag]`

## Docker

### Mounting a file share

For example the below command runs an Ubuntu container with a root `/code` folder pointing to the `c:\dev\gitlab` host directory

```bash
docker run -v c:\dev\gitlab:/code ubuntu
```
