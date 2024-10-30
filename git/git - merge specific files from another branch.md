# git - How to "merge" specific files from another branch
explained nicely on : https://jasonrudolph.com/blog/2009/02/25/git-tip-how-to-merge-specific-files-from-another-branch/


- can just use `git checkout`

```
git checkout feature_branch1 <paths>...
```

we can simply give git checkout the name of the feature_branch1 and the paths to the specific files that we want to add to our master branch.

```
$ git branch
```
shows you are on master
* master
feature_branch1 

```
$ git checkout feature_branch1 folder/file_name1.txt folder/file_name2.txt 
```
note that if there is a fatal warning or it doesn't recognize the command, make sure you ad a ` -- ` (spaces included)  

```
$ git checkout feature_branch1 -- folder/file_name1.txt folder/file_name2.txt 
```

and it adds the files to your master ! (it doesn't have to be master, it can be any branch that you are working on)
