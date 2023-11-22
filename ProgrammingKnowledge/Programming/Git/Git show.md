
Shows to diff of a commit.  It also supports pretty printing like [[Git log]] .


```
git show head --pretty='parent %Cred%p%Creset commit %Cred%h%Creset%C(yellow)%d%Creset%n%n%w(72,2,2)%s%n%n%w(72,0,0)%C(cyan)%an%Creset %Cgreen%ar%Creset'

git config --global alais.so "show head --pretty='parent %Cred%p%Creset commit %Cred%h%Creset%C(yellow)%d%Creset%n%n%w(72,2,2)%s%n%n%w(72,0,0)%C(cyan)%an%Creset %Cgreen%ar%Creset'""

```

### Read commit meta data

```
git show head --no-patch
```


### Get a summary of a commit

```
git show head --stat
```



#Git 