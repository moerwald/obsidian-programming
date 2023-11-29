
## Branch model

Show branches with their corresponding commit hash:

```
git show-ref --heads
```

![[Pasted image 20231129081436.png]]


### Delete branch

```
git branch -d branchName
```

`-D` forces branch deletion **even** there are **unmerged** commits.

>[!note]
Branch deletion only deletes the branch **reference**, the commit is still available. In this case the commit is in state `dangling`, which means there is no direct reference to that commit.

Show dangling commits via:


![[Pasted image 20231129082040.png]]

### Recreate a branch

```
git branch branchName commitHash
```


## Kinds of Branches

Normally you've two kinds of branches:

- Long-running branch, or
- Topic branch

#### Long-running branch


![[Pasted image 20231129082510.png]]

#### Topic branch

![[Pasted image 20231129082607.png]]


#### Public vs private branches

Public branches are the ones that are published to another repo, so other devs can use them.

Private branches are **not** published -> here you can rewriter history without any worries.

## Ways of Merging

![[Pasted image 20231129082939.png]]


![[Pasted image 20231129083052.png]]

![[Pasted image 20231129083137.png]]

#### Rebase

![[Pasted image 20231129083300.png]]


![[Pasted image 20231129083553.png]]


## Cherry-pick

![[Pasted image 20231129083712.png]

![[Pasted image 20231129083856.png]]

### Cherry-pick multiple commits

>[!tip]
>Get the commit where a branch was created from: `git merge-base master feature-branch`



![[Pasted image 20231129084251.png]]

Alias to cherry pick multiple commits in an easy way:

![[Pasted image 20231129084627.png]]

![[Pasted image 20231129084645.png]]


## Resolving conflicts




#Git




