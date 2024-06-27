# The following untracked working tree files would be overwritten by merge

How would I deal with this message and overwrite those files, without having to find, move or delete those files myself?

The problem is that you are not tracking the files locally, but identical files are tracked remotely.
In order to "pull" your system would be forced to overwrite the local files which are not version controlled.

Try running
```
git add *
git stash
git pull
```

This will track all files, remove all of your local changes to those files, and then get the files from the server.
