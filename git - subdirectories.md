
Note that Git does not consider adding an empty directory to be a change. This is because GIT tracks only changes to files, not changes to directories. 

But sometiems you want an empty directory as a placeholder, so you can create an empty file often called `.git-keep` in a placeholder directory.

```
touch CSS/.git-keep
git add CSS
```
