# How to undo a Git commit that was not pushed
Source: https://bytefreaks.net/programming-2/how-to-undo-a-git-commit-that-was-not-pushed

To undo a Git commit that was not pushed, you are given a few major options:
## Method 1: Undo commit and keep all files staged
In case you just want to undo the commit and change nothing more, you can use

```
git reset --soft HEAD~
```
This is most often used to make a few changes to your latest commit and/or fix your commit message. Leaves working tree as it was before reset.
soft does not touch the index file or the working tree at all (but resets the head to the previous commit). This leaves all your changed files Changes to be committed, as git status would put it.

## Method 2: Undo commit and unstage all files
In case you want to undo the last commit and unstage all the files you can use the following

```
git reset HEAD~
#or
git reset --mixed HEAD~
```
mixed will reset the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the default action.

## Method 3: Undo the commit and completely remove all changes
The following method will undo the commit and revert all changes so that your state is exactly as it was before you started making changes.

```
git reset --hard HEAD~
```
