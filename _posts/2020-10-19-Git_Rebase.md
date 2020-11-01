---
title: "Git Rebase - Cherry-pick / Upstream"
categories:
  - Git
tags:
  - git
---

# Rebase

## git pull -r
- syncronize with remote branch and rebase  

## cherry-pick
- 다른 브랜치에 있는 커밋을 선택적으로 내 브랜치에 적용
- **git-cherry-pick - Apply the changes introduced by some existing commits**  
    - What *git cherry-pick* does is it takes the commit that you specify and reads the difference between it and it's parent. This effectively makes a patch. It then applies this patch to your currently checked out branch.  
    - You cherry pick a commit, the commit contains 1 change in 1 file  

- `--no-commit`  
  - The --no-commit option will execute the cherry pick but instead of making a new commit it will move the contents of the target commit into the working directory of the current branch.
  - Usually the command automatically creates a sequence of commits. This flag applies the changes necessary to cherry-pick each named commit to your working tree and the index, without making any commit. In addition, when this option is used, your index does not have to match the HEAD commit. The cherry-pick is done against the beginning state of your index.
  - This is useful when cherry-picking more than one commits' effect to your index in a row.

## git branch upstream
```shell
$ git branch -u origin/master
$ git rebase
```
- 내 personal branch가 master 를 가리키게 set
- __-u < upstream >__
    - --set-upstream-to= < upstream >
    - Set up < branchname >'s tracking information so < upstream > is considered < branchname >'s upstream branch. If no < branchname > is specified, then it defaults to the current branch
    - When you checkout a branch in git from a remote repository such as github or bitbucket, the “upstream branch” is the remote branch hosted on github or bitbucket (or other remote source)
    - Upstream branches define the branch tracked on the remote repository by your local remote branch (also called the remote tracking branch) When creating a new branch, or when working with existing branches, it can be quite useful to know how you can set upstream branches on Git.  


```shell
$ git branch --set-upstream < remote-branch >
```

* sets the default remote branch for the current local branch.

* Any future git pull command (with the current local branch checked-out), will attempt to bring in commits from the < remote-branch > into the current local branch.