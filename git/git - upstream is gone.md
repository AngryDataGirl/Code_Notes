
https://stackoverflow.com/questions/21609781/why-call-git-branch-unset-upstream-to-fixup


1. I have created an empty (new) repo using git init --bare on one of my servers. 
2. Then I have git cloned it to a local workspace on my PC.
3. After committing a single version on the local repo I got that error after calling git status.
4. What happens is that the first commit on local working directory repo created "master" branch. But on the remote repo (on the server) there was never anything, so there was not even a "master" (remotes/origin/master) branch.
5. You can ignore the error and just run a `git push origin master` from local repo. This stops the error from appearing.

So to conclude - one may get such an error for a fresh new remote repo with zero commits since it has no branch, including "master".