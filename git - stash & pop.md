
When you pull changes before committing your own, you might encounter this error:

> **Please commit your changes or stash them before you can merge.**
  
This is git warning you that the pull will overwrite your version of a file, because someone else modified the same file.

*(you should generally stash or commit before pulling)*

  
1. use `git diff origin -- index.html` to check that changes don't overlap
2. `git stash` to save the state of the working tree and index by making a couple temporary commits (ie, saving your work while you do something else) without making a real commit or affecting your repository history
3. now it is safe to pull (in fact, git stash is shorthand for git stash push. It's a lot like the stack where you put bills that you haven't gotten around to paying yet) so run `git pull` and then `git stash pop`

  Popping the stash merges the changes. If changes overlap, there might be a conflict.

  

