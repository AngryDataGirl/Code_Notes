- [git add](#git-add)
  - [git add -a](#git-add--a)


## working tree 

 The set of nested directories and files that contain the project that's being worked on.

```
ls -la
```
you should ensure that there is a subdirectory named `.git` here

## git status

#git status displays the state of the working tree and of the staging area. It lets you see which changes are currently being tracked by Git, so you can decide whether you want to ask Git to take another snapshot.
```
git status
```

## git diff

after modifying a file, you can see what's changed with git diff

```
git diff
git diff HEAD^
```

will produce output if the working tree, index and head are NOT in agreement


# git add

git add is the command you use to tell Git to start keeping track of changes in certain files.

The technical term is staging these changes. You'll use git add to stage changes to prepare for a commit. All changes in files that have been added but not yet committed are stored in the staging area.

```
git status
```

## git add -a

adds everything

```
git add .
```

adds files that are not staged for commit (ignores untracked)

```
add -u
```

Though, your .gitignore should prevent the untracked (and ignored) files from being shown in status, added using git add etc.

