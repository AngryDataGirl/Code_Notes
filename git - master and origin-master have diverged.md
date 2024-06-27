master branch and 'origin/master' have diverged, how to 'undiverge' branches'?

# Quick and Dirty 

```
git reset --hard origin/main
```

Then that just resets my (local) copy of main (which I assume is screwed up) to the correct point, as represented by (remote) origin/main.
WARNING: You will lose all changes not yet pushed to origin/main.

# Rebase
If origin is up-to-date, then some commits have been pushed to origin from another repo while you made your own commits locally.
You based commit C on commit A because that was the latest work you had fetched from upstream at the time.
However, before you tried to push back to origin, someone else pushed the commit B.

Development history has diverged into separate paths. And looks like this:
```
... o ---- o ---- A ---- B  origin/main (upstream work)
                   \
                    C  main(your work)
```

```
$ git rebase origin/main
```

old repositories
```
$ git rebase origin/master
```

This tells Git to replay commit C (your work) as if you had based it on commit B instead of A.
Git just adds explicit separation between the commit and rebase steps.

The graph of history now looks like this:
```
... o ---- o ---- A ---- B  origin/main (upstream work)
                          \
                           C'  main (your work)
```  
Commit C' is a new commit created by the git rebase command.

It is different from C in two ways:
- It has a different history: B instead of A.
- Its content accounts for changes in both B and C; it is the same as M from the merge example.

Note that the history behind C' is still linear.

An attempt to push C' into our repository will work (assuming you have permissions and no one has pushed while you were rebasing).

The git pull command provides a shorthand way to fetch from origin and rebase local work on it:
```
$ git pull --rebase
```
This combines the above fetch and rebase steps into one command.
