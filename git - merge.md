#git/commit #git/push #git/merge

## General workflow

Where <branch_name> is the branch you want to merge into master.
this flow assumes there are no conflicts with master.

```
git checkout master
git fetch
git pull
git checkout <branch_name>
git merge master
```

> there are conflicts

6. open the conflicting files
7. fix the conflicts in the file, save it
8. proceed to no conflicts section

> no conflicts

```
git add .
git commit -m "insert comment here"
git push -u origin <branch_name>
```


## Options for addresing addressing merge conflicts

- `git merge --abort` to restore the main branch to what it was before the merge , run `git pull` to get latest changes, create a new branch, make their changes and merge their breanch into the main branch
- `git reset --hard` to get back to where they were before they started the merge
- resolve conflict manually by using information git inserts into the affected files (preferred), resolve manually in file, save file and then run following commands to commit the change

  