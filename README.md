# Useful commands

* [Git](#git)
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

### Git commands

#### Add

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

## Docker

### Mounting a file share

For example the below command runs an Ubuntu container with a root `/code` folder pointing to the `c:\dev\gitlab` host directory

```bash
docker run -v c:\dev\gitlab:/code ubuntu
```