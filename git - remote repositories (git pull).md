 #git   

# remote repositories (git pull)

- when git clones a repo, it creates a ref to the original repo that's called a _remote_ by using the name origin

- it sets up the cloned repo so that the clone will _pull_ or retrieve data from the _remote_, it is very efficient because it only copies the new commits and objects from the remote and then checks them into your working tree

- `git pull` is a combination of two simpler operations `git fetch` and `git merge`

  

## create pull requests (git request-pull)

you submit a pull request to ask owner of the repo to pull changes into the main code base

  

```

git request-pull -p origin/main .

```

  

## complete pull request

- to complete the pull you have to set up a remote by using the `git remote` command

  
  

```

git add x

git commit -a -m "fix conflict"

git push

```