added stuff to [[Git]]

# Git
## How does Git Work?
All these commits are bound to a **branch**. Any new commits made will be added to this branch. A branch always points to the latest commit. The pointer to the latest commit is known as **HEAD**

### git rebase

- Should be used on local branches, since history does change and will be confusing for other team members
- Does not create any new commit, and results in a cleaner history
- The history is based on common commit of the two branches (base)
- The destination's branch commit is pulled from it's "base" and "rebased" on to the latest commit on the source branch
*cleaner but you loose history*
```bash
git checkout <featureBranch>

git rebase master
```


### Merge Conflicts
Merge conflicts occur when we try to merge two branches, which have the same file updated by two different developers. 

### How to resolve Merge Conflicts
The merge tool looks something like this, the top leftmost column is for Dev1 Branch changes, the centre column is for the original code i.e the master's code before any commits, and the right most column are the dev 2 branch changes. The area below these columns is where we make the changes, this is the place where we have the merged code.
![[Pasted image 20230815095935.png]]


### Git Workflow
A Git Workflow is a recipe or recommendation for how to use Git to accomplish work in a consistent and productive manner. Git workflows encourage users to leverage Git effectively and consistently.

There are the three popular workflows which are accepted and are followed by various tech companies:


Centralized Workflow

Feature Branching

GitFlow Workflow

