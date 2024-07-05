- [View branches](#view-branches)
- [Create branches](#create-branches)
- [checking out branches](#checking-out-branches)
- [Naming branches](#naming-branches)
- [renaming local git branches](#renaming-local-git-branches)
- [Updating pointer to remote](#updating-pointer-to-remote)
- [How to transfer changes to a new branch if you forgot to create one](#how-to-transfer-changes-to-a-new-branch-if-you-forgot-to-create-one)
  - [If you have not yet committed:](#if-you-have-not-yet-committed)
  - [If you've already committed:](#if-youve-already-committed)
- [deleting a branch](#deleting-a-branch)
  - [delete a local branch](#delete-a-local-branch)
  - [delete a remote branch](#delete-a-remote-branch)

## View branches

-a shows all local and remote branches 
-v verbose shows commit subject line for each head 

```
git branch -av  
```

list all remote branches

```
git branch -r
```

## Create branches

```
git checkout -b [your new branch name here]
```

create branch from master

```
git checkout -b new-branch master
```

create branch as a sub branch of another branch

1. Checkout or change into "branch1"

 `git checkout branch1`

2. Now create your new branch called "subbranch_of_b1" under the "branch1" using the following command.

 `git checkout -b subbranch_of_b1 branch1``

3. The above will create a new branch called subbranch_of_b1 under the branch branch1 (note that branch1 in the above command isn't mandatory since the HEAD is currently pointing to it, you can precise it if you are on a different branch though).

Now after working with the subbranch_of_b1 you can commit and push or merge it locally or remotely.

## checking out branches

```
git checkout -branch_name
```
where branch name is the name of the branch you want to checkout (get the name of the branch by listing all branches above)


## Naming branches 

To set the name of default branch, initialize your new repository and set the name of the default branch to main:

```
git init --initial-branch=main
git init -b main
```
or
```
git init
git checkout -b main
```

## renaming local git branches

Before we begin, make sure you’ve selected the branch you want to rename. Run this command to do so:
 
```sql
git checkout old-name
```

Replace `old-name` with the name of the appropriate branch.

```sql
git branch -m **new**-name
```
  
Alternatively, you can rename a local branch by running the following commands:

```sql
git checkout master
```

Then, rename the branch by running:  

```sql
git branch -m old-name **new**-name
```
  
Verify that the renaming was successful:
 
```sql
git branch -a
```

## Updating pointer to remote 

Telling git which remote branch to track, either because name changed or other. This will link your local to the upstream remote branch.

```
git branch --set-upstream-to origin/main
```

## How to transfer changes to a new branch if you forgot to create one

How we got here:
1. started working without creating a new branch
2. now you have a branch with commits and new changes, but a version of it has already been merged to main 
3. you need to create a new branch with your new changes
   
[https://stackoverflow.com/questions/44728962/forgot-to-create-new-branch-how-to-transfer-changes-to-new-branch](Stack Overflow Where I found the Answer)

### If you have not yet committed:

Then there is no harm in switching to a new branch after files have been modified. Edited, non-committed files (whether staged for commit or not) are always viewed in the context of whatever branch is checked out:

```
git checkout -b mytopicbranch
```

### If you've already committed:

Following the description: [here](https://lostechies.com/derickbailey/2010/06/08/git-d-oh-i-meant-to-create-a-new-branch-first/):

1. Create the branch you wished you had made (but don't switch to it):

```
git branch mytopicbranch
```

It now has all the commits that you wanted to make.

2. Reset the master branch back to before these commits:

```
git reset abc5b0de1 --hard
```

Assuming `abc5b0de1` is the fingerprint of the commit right before you made the accidental commits.

Now you can switch back to `mytopicbranch` as needed.

## deleting a branch

-D to force delete

```
git branch -d <branch_name>
git branch -D <branch_name>
```
### delete a local branch

1. list all branches

    ```
    git branch -a
    ```

    It is not possible to delete a branch you are currently in and viewing. You will get an error. 

Before deleting a local branch, switch to a branch **you do NOT want to delete**:

```
git checkout branch_name
```

  1. delete the branch using this command.

```
git branch -d local_branch_name

```

If the branch contains unmerged changes and unpushed commits, the `-d` flag ill not allow local branch to be deleted

this is because commits are not seen by any other branches and git is protecting you from accidentally losing any commit data


if you still want to delete and are ABSOLUTELY SURE because there is no prompt asking you to confirm your actions

1. `-D` flag must be used

```

git branch -D local_branch_name

```
### delete a remote branch

Remote branches are separate from local branches. They are repositories hosted on a remote server that can be accessed there. Local branches are repositories on your local system.

You don’t use `git branch`command that you use for local branches, instead you delete remote branches with the `git push` command. You’ll need to specify the name of the remote which is usually `origin`.

1. list all remote branches

    ```yaml

    git branch -r

    ```

2. remote branches will show as g`remote/origin/branch1` and `remote/origin/branch2`
    1. where remote name is `origin`
    2. and remote branch name is `branch1`

    ```yaml

    git push remote_name -d remote_branch_name

    ```