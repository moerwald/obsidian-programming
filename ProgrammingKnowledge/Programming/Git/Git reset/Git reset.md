
Deletes unused commits.

```
git reset --hard HEAD~2
```

Removes the last two commits. `--hard` resets the index and the working copy, to reflect the state of the commit to be reset to.

### --hard

>[!Warn]
>`--hard` Moves `Head` to the given commit and resets the Index and Working Directroy to match the given commit.

![[Pasted image 20231126212229.png]]

### --mixed

`--mixed`. which is the default, will unstage changes from the previous commit.

![[Pasted image 20231126212342.png]]
### --soft

>[!Tip]
>`--soft` keeps the index and the working copy.

![[Pasted image 20231126212405.png]]

For the difference between `--mixed` and `--soft` see this [link](https://stackoverflow.com/questions/3528245/whats-the-difference-between-git-reset-mixed-soft-and-hard) .



#Git 
