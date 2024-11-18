Q: master branch and 'origin/master' have diverged, how to 'undiverge' branches'?

# Quick and Dirty Way

Resets the local copy of main / master (which is messed up) to the original remote origin/main.
```
git reset --hard origin/main
```

# Rebase versus Merge 

It's simple. With rebase you say to use another branch as the new base for your work. If you have, for example, a branch master, you create a branch to implement a new feature, and say you name it cool-feature, of course, the master branch is the base for your new feature. Now, at a certain point, you want to add the new feature you implemented in the master branch. You could just switch to master and merge the cool-feature branch:

```
$ git checkout master
$ git merge cool-feature
```
But this way a new dummy commit is added. If you want to avoid spaghetti-history you can rebase:

```
$ git checkout cool-feature
$ git rebase master
```

And then merge it in master:

```
$ git checkout master
$ git merge cool-feature
```

This time, since the topic branch has the same commits of master plus the commits with the new feature, the merge will be just a fast-forward.

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
