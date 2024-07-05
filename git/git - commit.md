#git 
**git commit -m**  

Commit is both a verb and a noun.

- verb, committing changes means you put a copy (of the file, directory, or other "stuff") in the repository as a new version.
- noun, a commit is the small chunk of data that gives the changes you committed a unique identity. The data that's saved in a commit includes the author's name and e-mail address, the date, comments about what you did (and why), an optional digital signature, and the unique identifier of the preceding commit.

```
git commit -m "[insert commit message here]"
```

**combined git add and commit**

```
git commit -am "comment"
```

 **see list of commits**

```
git log --oneline
```

**git log**

```
  git log -- A
```

The git log command allows you to see information about previous commits. Each commit has a message attached to it (a commit message), and the git log command prints information about the most recent commits, like their time stamp, the author, and a commit message. 

This command helps you keep track of what you've been doing and what changes have been saved.