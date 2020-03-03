# Useful commands

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

### Git commands

#### Add

`git add -p` (for partial) allows to add part of a modified file. Git will display hunks of the file one by one and ask if you want to add them

```bash
git add -p
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

## Docker

### Mounting a file share

For example the below command runs an Ubuntu container with a root `/code` folder pointing to the `c:\dev\gitlab` host directory

```bash
docker run -v c:\dev\gitlab:/code ubuntu
```