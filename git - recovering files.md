 #git 
 ## recovering a deleted file that was removed with rm

  

1. delete a file

```

rm file.html

```

2. use an `ls` command to verify that file.html was deleted

```

ls

```

3. recover the file

```

git checkout -- file.html

```

## recover file deleted with : git rm

  

```

git rm file.html

```

when you use git rm - it deletes the file but also records the deletion in the index

so you have to unstage the deletion with

```

git reset HEAD file.html

```

and recover

```

git chekcout -- file.html

```