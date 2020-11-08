---
title: "Git - refs"
categories:
  - Git
tags:
  - git
---

## Git refs/for
> **git push [option] [ < repository > [< refspec >]]**  

## refs
* git은 모든 커밋을 Key-Value 형태로 관리
* key는 SHA-1으로 만들어진 40자리의 해시값
* 쉬운 이름의 파일(References)에 해시값이 저장
    *  `.git/refs`

* 모든 refs는 .git/refs에 저장 
* 하위에는 heads, remotes, tags 디렉토리가 존재  

```shell
$ pwd
.git/refs

$ ls
heads/  remotes/  tags/

$ cd
heads/

$ ls
master

$ cat master
6aeawerdfgdfg861145f19sdfafetrgf80af91
```

* master 브랜치가 바로 refs
* git 에서는 어떤 특정한 작업을 가리키는 refs를 **브랜치**라고 부름

## refs/for in Gerrit
> [Gerrit Documentation](https://gerrit-review.googlesource.com/Documentation/)


When pushing a new or updated commit to Gerrit, you push that commit using a reference, in the refs/for namespace. This reference must also define the target branch, such as `refs/for/[BRANCH_NAME]`.

For example, to create a new change on the master branch, you would use the following command:
```shell
$ git push origin HEAD:refs/for/master
```
The `refs/for/[BRANCH_NAME]` syntax allows Gerrit to differentiate between commits that are pushed for review and commits that are pushed directly into the repository.

* refer to
    * [why using refs/for in gerrit](https://stackoverflow.com/questions/10461214/why-is-git-push-gerrit-headrefs-for-master-used-instead-of-git-push-origin-mast)