
>[!note]
Git `Index` = `Staging Area`.  `Working Directory` -> were you edit your files. After the change you've to add it to the `Index`.


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


#Git 