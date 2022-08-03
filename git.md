# Git commands

Install Git on mac

    $ brew install git

Get Git version

    $ git --version

Get help from Git

    $ git help

Get help for a command

    $ git help <command>

Configure username and email in git

    $ git config --global user.name "<user name>"

    $ git config --global user.email "<user email>"

View or update global git config

    $ git config --global -e

Change default branch name

    $ git config --global init.defaultBranch <branch name>

Initialize a repository

    $ git init

View branch status

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

Get the list of branches

    $ git branch

Rename a branch

    $ git branch -m <current name> <new name>

Add to stage and commit

    $ git commit -am <comment>

View repository logs

    $ git log

Add files of the same extension to stage with a wildcard

    $ git add *.<extension>

    $ git add <path>/*.<extension>

    $ git add file/

File to track a directory ".gitkeep"

Create an alias of a command

    $ git config --global alias.<alias name> '<command>'

Git diff

    $ git diff

    $ git diff --staged

Fix last commit comment

    $ git commit --amend -m <comment>

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