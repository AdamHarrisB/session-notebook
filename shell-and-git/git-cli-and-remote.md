Git CLI

You can create git repositories and commits locally. You can also synchronize your local repository with a remote repository (i.e. on GitHub).

Creating a local repository:

Navigate into the folder you'd like to turn into a repository and run:

    git init

DON'T initialize a git repository inside another git repository. You can check the status of a folder, you can run:

    git status

Displaying either

    fatal: not a git repository (or any of the parent directories): .git

or

    On branch main
    nothing to commit, working tree clean

States of Files

Untracked - Not added to Git
Modified - Has changes since the last commit
Staged - Is included in the next commit
Committed - All changes have been saved in git

Committing in a Local Repository

Try submitting these commands for each completed change:

git status - list files that have changed
git add - add files to the stage
git commit -m "message" - create a commit including all staged files
git log --oneline - show the commit history

Using Commits as Backups

You can always return to the last committed state using:

git restore .

You can also restore individual files:

git restore <filename>

Connecting to a Remote Repository

This enables teams to work on the same remote repository and clone it locally. The remote repository also serves as a backup.

Connecting Your Local Repository to a New Remote Repository

The first thing to do is to create a new empty remote repository on GitHub. You will then see some hints "...or push an existing repository from the commmand line." Copy the commands from GitHub and execute them in your local project folder.

git remote add origin git@github.com:GitHubUsername/repository-name.git
git branch -M main
git push -u origin main

Cloning a Remote Repository

You can create a copy of the remote repository on your local machine with the following command:

git clone <url>

Synchronizing Local and Remote Repositories

git push - Upload to the remote repository
git pull - Download content from the remote repository