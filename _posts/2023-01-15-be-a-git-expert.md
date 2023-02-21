---
layout: post
title:  "To be a Git Expert"
date:   2023-01-15 16:25:50 +0800
category: tech
---

## Git basic

- Create or clone a git repo by using `git init` or `git clone`
- Add local changesd files or folders to *stage area* `git add`
- Commit change in *stage area* to *local repository* `git commit`
- Update local change to remote repo by using `git push`
- Get remote update to local by using `git pull`
- Resovle merge conflict by fixing confict content.  `<<< to ===` are local change, and `=== to >>>` are remote change

> [Best Practie of Git Commit](https://gist.github.com/luismts/495d982e8c5b1a0ced4a57cf3d93cf60)

## Git branch

### checkout/merge between different branch

```shell
➜  01_workspace  mkdir git
➜  01_workspace  cd git
➜  git  mkdir branch_tutorial
➜  git  cd branch_tutorial
➜  branch_tutorial  pwd
/Users/calviny/Documents/01_work/01_workspace/git/branch_tutorial
➜  branch_tutorial  git init
Initialized empty Git repository in /Users/calviny/Documents/01_work/01_workspace/git/branch_tutorial/.git/
➜  branch_tutorial (master) code .
➜  branch_tutorial (master) ls                                                                                      ✱
myfile.txt
➜  branch_tutorial (master) git add myfile.txt                                                                      ✱
➜  branch_tutorial (master) git commit -m "first commit"                                                            ✈
[master (root-commit) 6c1a458] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 myfile.txt
➜  branch_tutorial (master) git branch issue1
➜  branch_tutorial (master) git branch
➜  branch_tutorial (master) git checkout issue1
Switched to branch 'issue1'
➜  branch_tutorial (issue1) git add myfile.txt
➜  branch_tutorial (issue1) git commit -m "with add comments"                                                       ✈
[issue1 a07cf02] with add comments
 1 file changed, 2 insertions(+), 1 deletion(-)
➜  branch_tutorial (issue1) git branch
➜  branch_tutorial (issue1)
➜  branch_tutorial (issue1) git checkout master
Switched to branch 'master'
➜  branch_tutorial (master) git merge issue1
Updating 6c1a458..a07cf02
Fast-forward
update with pull comments
 myfile.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
➜  branch_tutorial (master) git branch -d issue1
Deleted branch issue1 (was a07cf02).
➜  branch_tutorial (master) git branch issue2
➜  branch_tutorial (master) git branch issue3
➜  branch_tutorial (master) git checkout issue2
Switched to branch 'issue2'
➜  branch_tutorial (issue2) git add myfile.txt
➜  branch_tutorial (issue2) git commit -m "update with commit comments"                                             ✈
[issue2 bd7e41f] update with commit comments
 1 file changed, 2 insertions(+), 1 deletion(-)
➜  branch_tutorial (issue2) git branch issue3
fatal: a branch named 'issue3' already exists
➜  branch_tutorial (issue2) git checkout issue3
Switched to branch 'issue3'
➜  branch_tutorial (issue3) git add myfile.txt
➜  branch_tutorial (issue3) git commit -m "update with pull comments"                                               ✈
[issue3 1920d58] update with pull comments
 1 file changed, 2 insertions(+), 1 deletion(-)
➜  branch_tutorial (issue3) git checkout master
Switched to branch 'master'
➜  branch_tutorial (master) git merge issue2
Updating a07cf02..bd7e41f
Fast-forward
 myfile.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
➜  branch_tutorial (master) git merge issue3
Auto-merging myfile.txt
CONFLICT (content): Merge conflict in myfile.txt
Automatic merge failed; fix conflicts and then commit the result.
➜  branch_tutorial (master) git add myfile.txt                                                                      ✂
➜  branch_tutorial (master) git commit -m "merge issue3 branch"                                                     ✈
[master 97a11f2] merge issue3 branch
➜  branch_tutorial (master)
➜  branch_tutorial (master) git reset --hard HEAD~
HEAD is now at bd7e41f update with commit comments
➜  branch_tutorial (master) git checkout issue3
Switched to branch 'issue3'
➜  branch_tutorial (issue3) git rebase master
Auto-merging myfile.txt
CONFLICT (content): Merge conflict in myfile.txt
error: could not apply 1920d58... update with pull comments
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply 1920d58... update with pull comments
➜  branch_tutorial (bd7e41f) git add myfile.txt                                                                     ✂
➜  branch_tutorial (bd7e41f) git rebase --continue                                                                  ✈
[detached HEAD b9f5424] update with pull comments
 1 file changed, 2 insertions(+), 1 deletion(-)
Successfully rebased and updated refs/heads/issue3.
➜  branch_tutorial (issue3) git checkout master
Switched to branch 'master'
➜  branch_tutorial (master) git merge issue3
Updating bd7e41f..b9f5424
Fast-forward
 myfile.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
➜  branch_tutorial (master) git checkout issue2
Switched to branch 'issue2'
➜  branch_tutorial (issue2) git merge master
Updating bd7e41f..b9f5424
Fast-forward
 myfile.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
➜  branch_tutorial (issue2) git checkout master
Switched to branch 'master'
```


## Git tag

```shell
➜  git  mkdir tag_tutorial
➜  git  cd tag_tutorial
➜  tag_tutorial  git init
Initialized empty Git repository in /Users/calviny/Documents/01_work/01_workspace/git/tag_tutorial/.git/
➜  tag_tutorial (master) ls
myfile.txt
➜  tag_tutorial (master) git add myfile.txt                                                                         ✱
➜  tag_tutorial (master) git commit -m "first commit"                                                               ✈
[master (root-commit) c281467] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 myfile.txt
➜  tag_tutorial (master) git tag apple
➜  tag_tutorial (master) git tag
➜  tag_tutorial (master) git log --decorate
➜  tag_tutorial (master) git tag -am "second tag" banana
➜  tag_tutorial (master) git tag -n
➜  tag_tutorial (master) git tag -d banana
Deleted tag 'banana' (was 562d62f)
➜  tag_tutorial (master) git tag -n
```

## Change git commit

- `mixed` mode: restore changed index
- `hard` mode: completely remove recent commit content
- `soft` mode: only cancel commit

### How to rollback at different phases

```shell
➜  tutorial3 (master) cd ../tutorial1
➜  tutorial1 (master) ls
sample.txt
➜  tutorial1 (master) git add sample.txt
➜  tutorial1 (master) git status                                                                                    ✈
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   sample.txt

➜  tutorial1 (master) git restore --staged sample.txt                                                               ✈
➜  tutorial1 (master) git status                                                                                    ✭
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   sample.txt

no changes added to commit (use "git add" and/or "git commit -a")
➜  tutorial1 (master) git add sample.txt                                                                            ✭
➜  tutorial1 (master) git log                                                                                       ✈
➜  tutorial1 (master) git status                                                                                    ✈
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   sample.txt

➜  tutorial1 (master) git commit -m "add pull comments"                                                             ✈
[master d4c778e] add pull comments
 1 file changed, 2 insertions(+), 1 deletion(-)
➜  tutorial1 (master) git status
On branch master
nothing to commit, working tree clean
➜  tutorial1 (master) git log
➜  tutorial1 (master) git reset --hard HEAD~
HEAD is now at 613b380 添加add and commit Comments
➜  tutorial1 (master) git log
➜  tutorial1 (master) git push --force
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
 + 0707ca7...cf98351 master -> master (forced update)
```

### cherry-pick

```shell
➜  tutorial3 (master) cd ../tutorial4
➜  tutorial4 (issue1) git log
➜  tutorial4 (issue1) git checkout master
Switched to branch 'master'
➜  tutorial4 (master) git checkout issue1
Switched to branch 'issue1'
➜  tutorial4 (issue1) git log
➜  tutorial4 (issue1) git checkout master
Switched to branch 'master'
➜  tutorial4 (master) git cherry-pick c81dba126bb0416c1b5c1bc9aa2943f28a0d6c82
Auto-merging sample.txt
CONFLICT (content): Merge conflict in sample.txt
error: could not apply c81dba1... add commit comments
hint: After resolving the conflicts, mark them with
hint: "git add/rm <pathspec>", then run
hint: "git cherry-pick --continue".
hint: You can instead skip this commit with "git cherry-pick --skip".
hint: To abort and get back to the state before "git cherry-pick",
hint: run "git cherry-pick --abort".
➜  tutorial4 (master) git add sample.txt                                                                            ✂
➜  tutorial4 (master) git commit                                                                                    ✈
[master a9c01cc] add commit comments
 Date: Mon Dec 15 15:05:35 2014 +0900
 1 file changed, 1 insertion(+)
➜  tutorial4 (master) git log
```

### merge -squash

```shell
/Users/calviny/Documents/01_work/01_workspace/git/stepup-tutorial/tutorial7
➜  tutorial7 (issue1) clear
Squashed commit of the following:
➜  tutorial7 (issue1) cd ..
➜  stepup-tutorial  cd tutorial7
➜  tutorial7 (issue1) git checkout master
Switched to branch 'master'
➜  tutorial7 (master) git merge --squash issue1
Auto-merging sample.txt
CONFLICT (content): Merge conflict in sample.txt
Squash commit -- not updating HEAD
Automatic merge failed; fix conflicts and then commit the result.
➜  tutorial7 (master) git add sample.txt                                                                            ✂
➜  tutorial7 (master) git commit -m "merge squash from branch:issue1"                                               ✈
[master 1d87327] merge squash from branch:issue1
 1 file changed, 2 insertions(+)
➜  tutorial7 (master) git log
➜  tutorial7 (master) git branch
➜  tutorial7 (master) git checkout issue1
Switched to branch 'issue1'
➜  tutorial7 (issue1) git log
➜  tutorial7 (issue1) git checkout master
Switched to branch 'master'
➜  tutorial7 (master) git log
➜  tutorial7 (master) git reset --hard HEAD~
HEAD is now at 007f89f 添加add的说明
➜  tutorial7 (master) git log
➜  tutorial7 (master) git merge --squash issue1
Auto-merging sample.txt
CONFLICT (content): Merge conflict in sample.txt
Squash commit -- not updating HEAD
Automatic merge failed; fix conflicts and then commit the result.
➜  tutorial7 (master) git add sample.txt                                                                            ✂
➜  tutorial7 (master) git commit                                                                                    ✈
[master 7ead666] Squashed commit of the following:
 1 file changed, 2 insertions(+)
➜  tutorial7 (master) git log
```

## Thanks To

- [Even Monkey can learn Git](https://backlog.com/git-tutorial/cn/)  :thumbsup:
- [Bilibili: Key points of learning Git/Github](https://www.bilibili.com/video/BV1KZ4y1e7cG/)
- [Game: Learn to branching](https://learngitbranching.js.org/)

