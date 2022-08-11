# Git commands

Install Git on mac

    $ brew install git

Get Git version

    $ git --version

Get help from Git

    $ git help

Get help for a command

    $ git help <command>

## Git config

Configure username and email in git

    $ git config --global user.name "<user name>"

    $ git config --global user.email "<user email>"

View or update global git config

    $ git config --global -e

Change default branch name

    $ git config --global init.defaultBranch <branch name>

Create an alias of a command

    $ git config --global alias.<alias name> '<command>'

## Git stage and commit

Initialize a repository

    $ git init

See current status

    $ git status

    $ git status --short

Add files to the stage

    $ git add <file name | -A | .>

Delete files from the stage

    $ git reset <file name | .>

Create a commit

    $ git commit -m <comment>

Go back to last commit

    $ git checkout -- .

Add to stage and commit

    $ git commit -am <comment>

View repository logs

    $ git log

Add files of the same extension to stage with a wildcard

    $ git add *.<extension>

    $ git add <path>/*.<extension>

    $ git add file/

File to track a directory ".gitkeep"

Git diff

    $ git diff

    $ git diff --staged

Fix last commit comment

    $ git commit --amend -m <comment>

## Git reset

Move to a previous commit without losing the changes

    $ git reset --soft <HEAD^ | hash>

Go back to a previous commit by removing everything from the stage

    $ git reset --mixed <HEAD^ | hash>

Go back to a previous commit removing changes

    $ git reset --hard <HEAD^ | hash>

Get git change reference in chronological order

    $ git reflog

Rename a file

    $ git mv <current name> <new name>

Delete a file

    $ git rm <file name>

Recover a recently deleted file

    $ git reset --hard

## Git branch

Show the list of branches

    $ git branch

Create a new branch

    $ git branch <branch name>

Create a new branch and move to the new branch

    $ git checkout -b <branch name>

Rename a branch

    $ git branch -m <current name> <new name>

Move to another branch

    $ git switch <branch name>

    $ git checkout <branch name>

Merge between branches

    $ git merge <branch name>

Delete a branch

    $ git branch -d <branch name>

Forcefully delete a branch

    $ git branch -d <branch name> -f

## Git tag

See the list of tags

    $ git tag

Create a tag

    $ git tag <tag name>

    $ git tag -a <tag name> -m <comment>

    $ git tag -a <tag name> <hash commit> -m <comment>

Show tag information

    $ git show <tag name>

Delete a tag

    $ git tag -d <tag name>

## Git stash

Save changes to the stash

    $ git stash

Save changes to the stash and give it a name

    $ git stash save <stash name>

Show stash detail

    $ git stash show <stash name>

See the stash list

    $ git stash list

Show the detail of each stash in the list

    $ git stash list --stat

Retrieve the last stash

    $ git stash pop

Retrieve a specific stash

    $ git stash apply <stash name>

Delete all stash

    $ git stash clear

Delete a specific stash

    $ git stash drop <stash name>

## Git rebase

Do a rebase

    $ git rebase <branch name>

Do an interactive rebase

    $ git rebase -i HEAD~<number of commits>