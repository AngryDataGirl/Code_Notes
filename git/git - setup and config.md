- [creating a .gitignore file](#creating-a-gitignore-file)
- [branches](#branches)
  - [set name of default branch](#set-name-of-default-branch)
  - [telling git which remote branch to track](#telling-git-which-remote-branch-to-track)


## checking #git version

```

git --version

```

  

## configure git, user, user email

```

git config --global user.name "<USER_NAME>"

git config --global user.email "<USER_EMAIL>"

git config --list

```

  

## make a directory

```

mkdir [insert directory_name]

cd [directory_name] # to navigate to directory

```

  

## initialize repo

  

- **Repository (repo):** The directory, located at the top level of a working tree, where Git keeps all the history and metadata for a project. Repositories are almost always referred to as repos. A bare repository is one that isn't part of a working tree; it's used for sharing or backup. A bare repo is usually a directory with a name that ends in .git—for example, project.git.

  

## clone a repository (git clone)

```

git clone

```

  

# creating a .gitignore file

Create the gitignore file.

```

code .gitignore

```

in the .gitignore file :

```

# to ignore files that have file names ending in .bak or ~.

*.bak

*~

  

# to ignore an entire directory

dir_to_ignore/

```

  

instead of .gitignore -- just exclude for yourself, update it in that file

  

```

cd .git

cd info

```

  

# branches

  

## set name of default branch

  

initialize your new repository and set the name of the default branch to main:

```

git init --initial-branch=main

git init -b main

```

or

```

git init

git checkout -b main

```

  

## telling git which remote branch to track

```

git branch --set-upstream-to origin/main

```

