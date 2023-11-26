
>[!note]
Git `Index` = `Staging Area`.  `Working Directory` -> were you edit your files. After the change you've to add it to the `Index`.

>[!Note]
>Stash -> an area were you can put changed files of the index and the working directory




To remove staged changes we can use

```
git reset HEAD
```

Which resets things to the `HEAD`-commit.

Alias

```
git config --global alias.unstage "reset HEAD"
```


### Add partial parts of file

```
git add --patch
```

You'll get an interactive view, were can choose which hunk shall be staged.


### Stash changes

Per default `git stash` stores changes in the working directory and the index to the stashing area.

```
git stash save --keep-index --include-untracked
```

Only stashes the working directory (incl. new untracked files)


### Reuse commit message from specific commit

```
git commit --ammed -C HEAD
```

Reuses the commit message of `HEAD`.
## Commit Message Format

Commit message should consist of:

- Short summary (max. 50 characters)
- Detailed description


#Git 