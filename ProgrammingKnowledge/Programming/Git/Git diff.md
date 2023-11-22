
>[!INFO] 
>Git diff shows diff between commits, while git show shows info about a specific commit.



Shows +/-10 lines about changed line.

```
git diff --unified=10
```


### Diff algorithms

Better diff output through different algorithms

```
git diff --patience

or 

git diff --histogram
```


Diff algorithm can be set via

```
git config --global diff.algorithm histogram
```


### Diff file only


Show diff of README.md since the last 3 commits.


```
git diff head~3:README.md..head:README.md
```

#Git