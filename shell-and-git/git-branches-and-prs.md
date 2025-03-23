Git Branches

When working on a project you want to work on features independently, without effecting other people's work. To do this we use branches on Git.

The common code base for a team is the main branch. To work on a new feature you:

    Create a new feature branch
    Commit your work on the new branch
    Finish work on the new feature, test functionality, and have other developers review your work.
    Merge your feature branch into the main branch.

Naming Branches

It is good practice for your branches to have short descriptive names, using hyphens as separators.

Git Branch Commands

    git switch -c <branchname> - create new branch and switch to it
    git branch - list your branches
    git branch a - list all branches (local and remote)
    git branch -d <branchname> - delete a branch

Git Pull Requests

GitHub offers us pull requests (PR) which we can use as convenient way to request reviews of the work on a feature branch.

A pull request is a request to  merge one branch into another branch. Other developers can review and request changes. If it is approved, we can merge the feature branch into the main branch.

Basic Workflow for a Pull Request

Create a new branch with git switch -c <branchname>
Make changes to the code
Push the changes and the new branch with git push origin <branchname> (once you have done this once, you can just use git push)
Create a pull request on GitHub
Share the pull request with your team
Review the pull request until it is approved
Merge the pull request into main
Pull the main branch to your local machine
Delete the new branch on GitHub and locally