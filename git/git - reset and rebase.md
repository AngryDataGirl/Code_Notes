Q: master branch and 'origin/master' have diverged, how to 'undiverge' branches'?

# Quick and Dirty Way

Resets the local copy of main / master (which is messed up) to the original remote origin/main.
```
git reset --hard origin/main
```

# Rebase

If you check origin and it is up to date -- then likely what happened was that commits were pushed to origin from another repo, while you were still committing locally. You based commit C on commit A because that was the latest work you had fetched from upstream at the time. However, before you tried to push back to origin, someone else pushed the commit B. This causes dev history to diverged into separate paths. And looks like this:
```
... o ---- o ---- A ---- B  origin/main (upstream work)
                   \
                    C  main(your work)
```

This tells Git to replay commit C (your work) as if you had based it on commit B (the latest origin) instead of A (the copy of origin that you had from upstream).

```
$ git rebase origin/main
```
Once you run that, the graph of history now looks like this:
```
... o ---- o ---- A ---- B  origin/main (upstream work)
                          \
                           C'  main (your work)
```  
Commit C' is a new commit created by the git rebase command.

It is different from C in two ways:
- It has a different history: B instead of A.
- Its content accounts for changes in both B and C; it is the same as M from the merge example.

Note that the history behind C' is still linear. An attempt to push C' into our repository will work (assuming you have permissions and no one has pushed while you were rebasing).

# Pull & Rebase 
The git pull command provides a shorthand way to fetch from origin and rebase local work on it:
```
$ git pull --rebase
```
This combines the above fetch and rebase steps into one command.
