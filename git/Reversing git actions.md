## Undo `git add` for uncommitted changes with:

```

git reset <file>

  

```

That will remove the file from the current index (the "about to be committed" list) without changing anything else.

  

## To unstage all changes for all files:

  

```

git reset

```

  

## reverting a commit

see only the most recent commit entry

```

git log -n1

```

use git revert to undo your committed changes

```

git revert --no-edit HEAD

```

`--no-edit` flag tells Git we don't want to add a commit message for this action

  

## undo the commit you just did

```

git reset --soft HEAD~1

git restore --staged [filename]

```