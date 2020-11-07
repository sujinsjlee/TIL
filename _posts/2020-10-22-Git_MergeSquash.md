---
title: "Git - Merge Squash"
categories:
  - Git
tags:
  - git
---

# Merge Squash
> 여러개의 커밋 로그를 하나로 묶기  

```shell
(master)$  git init
(master)$  git add .
(master)$  git commit -m 'initial file'
(master)$  git checkout -b feature

(feature)$  touch fileA
(feature)$  git add .
(feature)$  git commit -m 'feature file - A'

(feature)$  touch fileB
(feature)$  git add .
(feature)$  git commit -m 'feature file - B'

(feature)$  touch fileA
(feature)$  git add .
(feature)$  git commit -m 'feature file - C'

(feature)$  touch fileA
(feature)$  git add .
(feature)$  git commit -m 'feature file - D'

(feature)$  git log --oneline
4beaeec1 D
670fb04e C
93a666e1 B
d839f20a A
```
* __HEAD__ is currently pointing at D

## git reabase -i HEAD~3
>  Squash D,C,B into A


```shell
$ git reabase -i HEAD~3
```
* An editor will be fired up with all the commits in your current branch (ignoring merge commits), which come after the given commit. You can reorder the commits in this list to your heart’s content, and you can remove them. The list looks more or less like this:

```
pick d839f20a A
pick 93a666e1 B
pick 670fb04e C
pick 4beaeec1 D
...
```
* Update the file as below by refering option commands

```
r d839f20a A Changed
s 93a666e1 B
s 670fb04e C
s 4beaeec1 D
...
```
* Commands:
  * **p, pick** : use commit
  * **r, reword** : use commint, but edit the commit message
  * e, edit : use commit, but stop for amending
  * **s, squash** : use commit, but meld inro previous commit


## git merge --squash [branch name]
> multiple commits can be squashed by **git merge --squash [branch name]** command  



```shell
(feature_branch)$  touch a.txt
(feature_branch)$  git commit -m "A"

(feature_branch)$  touch b.txt
(feature_branch)$  git commit -m "B"

(feature_branch)$  touch c.txt
(feature_branch)$  git commit -m "C"

(feature_branch)$  touch d.txt
(feature_branch)$  git commit -m "D"

(feature_branch)$  git checkout master
(master)$  git merge --squash feature_branch
(master)$  git status
D
C
B
A

(master)$  git checkuot -b personal/test
(personal/test)$ git commit
```

* in above example, **git merge --squash [branch name]** will squash all commits different from master into one commit  
