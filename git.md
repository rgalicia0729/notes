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

Initialize a repository

    $ git init

Change default branch name

    $ git config --global init.defaultBranch <branch name>

View branch status

    $ git status

Add files to the stage

    $ git add <file name | -A | .>

Delete files from the stage

    $ git reset <file name | .>

Create a commit

    $ git commit -m "<comment>"

Go back to last commit

    $ git checkout -- .