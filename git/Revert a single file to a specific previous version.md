[git - How can I revert a single file to a previous version? - Stack Overflow](https://stackoverflow.com/questions/2733873/how-can-i-revert-a-single-file-to-a-previous-version)

Let's start with a qualitative description of what we want to do (much of this is said in Ben Straub's answer). We've made some number of commits, five of which changed a given file, and we want to revert the file to one of the previous versions. First of all, git doesn't keep version numbers for individual files. It just tracks content - a commit is essentially a snapshot of the work tree, along with some metadata (e.g. commit message). So, we have to know which commit has the version of the file we want. Once we know that, we'll need to make a new commit reverting the file to that state. (We can't just muck around with history, because we've already pushed this content, and editing history messes with everyone else.)

So let's start with finding the right commit. You can see the commits which have made modifications to given file(s) very easily:

```
git log path/to/file
```

If your commit messages aren't good enough, and you need to see what was done to the file in each commit, use the `-p/--patch` option:

```
git log -p path/to/file
```

Or, if you prefer the graphical view of gitk

```
gitk path/to/file
```

You can also do this once you've started gitk through the view menu; one of the options for a view is a list of paths to include.

Either way, you'll be able to find the SHA1 (hash) of the commit with the version of the file you want. Now, all you have to do is this:

```
# get the version of the file from the given commit
git checkout <commit> path/to/file
# and commit this modification
git commit
```

(The checkout command first reads the file into the index, then copies it into the work tree, so there's no need to use `git add` to add it to the index in preparation for committing.)

If your file may not have a simple history (e.g. renames and copies), see VonC's excellent comment. `git` can be directed to search more carefully for such things, at the expense of speed. If you're confident the history's simple, you needn't bother.