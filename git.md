#Git
I am learning Git CLI with [Learn Git Branching](http://learngitbranching.js.org/)!

## commit
```sh
$ git commit
```

## checkout
checking out a commit moves the HEAD location to that commit. ie. the checked out branch bugFix becomes our workspace. When you checkout using the hash value of a commit, you only need to type the hash until it is uniquely identifiable. Checking out a commit that does not have a branch name will detach the `HEAD` and make it point to that commit.
```sh
$ git checkout bugFix 
//or
$ git checkout fed2b 
```

#####Reference
Instead of typing in everything, you can also navigate through the history using Relative Refs (Parent `^` or Ancestor `~<num>`)
```sh
$ git checkout HEAD^
$ git checkout master~4 //moves HEAD to specified location
```	

##merge
```sh
$ git checkout master
$ git merge bugFix
```
the content of bugFix is copied into master. if master was the ancestor, copying bugFix into master would result in the same file as bugFix. So the master pointer would simply move to the bugFix location.

## [rebase](https://git-scm.com/book/ko/v1/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-Rebase%ED%95%98%EA%B8%B0)
> The second way of combining work between branches is rebasing. Rebasing essentially takes a set of commits, "copies" them, and plops them down somewhere else.

if I have C2 (master) and C3 (bugFix) in separate branches, I can rebase bugFix to master, which will result in the bugFix commit to become a child of the master branch. The command is as follows:
```sh
$ git checkout bugFix
$ git rebase master
```

#####the `-i` option
You can open a UI dialogue (works differently for different programs I guess) to select a point from where you choose which commits you want to rebase to HEAD. It's similar to cherry-pick but you can take a look at the descriptions or change the order of the commits.


## reset/revert
reset is usually for local, revert is usually for remote (shared) because revert leaves a history and people can see why and what you reverted.
reset simply moves the pointer to a previous commit, revert makes a new commit that is the opposite of the previous commit. 
```sh
$ git reset HEAD~1
$ git revert HEAD
```

## Branch Forcing
Move the reference (pointer) to a selected location
```sh
$ git checkout HEAD^
$ git checkout master~4 //moves HEAD to specified location
$ git branch -f master HEAD~3 //moves everything else except HEAD to specified location
$ git branch -f bugFix bugFix~3 //but not "git branch -f HEAD HEAD~3" because HEAD is not a branch. it can't be relocated.
```	

## Cherry picking
cherry-pick is a way to select as many commits as you want and copy it onto your current workspace.
```sh
$ git checkout master
$ git cherry-pick bugFix~5, bugFix~3, bugFix
```
this will copy the work you made in bugFix, ~3, and ~5 onto the master branch.

