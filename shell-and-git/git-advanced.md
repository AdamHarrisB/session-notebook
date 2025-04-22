Understanding Advanced Git Commands

git fetch

You can check whether your local branches are up to date with your remote repository, assigned the name "origin" by default, using git fetch.

If there is any difference:
    Git fetch will update the remote tracking branches
    This means that the local branch knows about all of the changes, but does not contain them yet.
    You still need to merge these changes manually, using git pull or git merge

git merge

To join two branches together, you can use git merge

Make sure that you:
    run git fetch first, should you want to merge the remote branch.
    switch to the branch where you want to incorporate the changes
    run git merge <branchname>

git merge is a fast-forward merge by default, and will not create a merge commit if the history is clean.

If a fast forward merge isn't possible, git merge will create a merge commit, incorporating the changes. To avoid this, and keep a clean history, you can use git rebase.

git pull

You can use git pull to fetch changes from a remote repository and merge them into the current branch

This is because git pull runs git fetch and then git merge.

git rebase

To join two branches together you can also use git rebase. Unlike git merge, it doesn't create a merge commit, resulting in a cleaner git history.

This strategy applies all of the changes of the branch we are rebasing to first, and then applies the changes of the branch we are rebasing from on top of it, by commit.

This is like replaying your latest changes on top of the changes from the other branch.

To rebase:
    Switch to the branch that should be changed
    Use the command git rebase main to incorporate changes from main into the branch
    If a conflict occurs
        Solve it in VS code, or on github presumably
        And then finish rebasing

How to solve conflicts

When you create a pull request to merge the feature branch into the main branch it can be the case that someone has already changed the lines of code you've been working on.

Conflicts in the code have to be solved manually by developers.

How to solve conflicts in VSCode

If a merge conflict occurs, you can use VSCode to solve it using the Source Control tab and identifying the files marked with a red exclamation mark. You can then choose to Accept Current Change, Accept Incoming Change, or Accept Both Changes.

Save the changes, and the continue with the git merge or rebase

How Common Conflicts Emerge

Scenario 1: Feature Branch differs from Main Branch

Either solve the conflict locally, or solve the conflict directly on GitHub.

Scenario 2: Fatal Error on Git Pull

This occurs when you have made at least one commit locally, someone else has committed to the branch that you intend to pull, and git isn't sure which came first.

To solve this conflict, follow these steps:

    git pull --no-ff
    resolve merge conflicts
    git commit -m "resolve merge conflict"
    git push

Solving Conflicts

Solving Conflicts locally

Option 1: git merge

If the feature branch has conflicts with the main branch you can use git merge to solve the conflict:

    Select the feature branch
    Use git merge main to merge the main branch into the feature branch
    The terminal then outputs the details of the conflict
    Resolve these conflict in VSCode
    Push the branch to GitHub
    You can then merge the pull request on GitHub

Option 2: git rebase

    Go to the feature branch
    Use git rebase main
    Resolve the merge conflicts
    Use git rebase --continue (a window will likely open for the merge commit request. Close this with :wq)
    git push --force-with-lease (this will protect the remote branch if it's different from the local branch)

Solving the conflict remote on GitHub

Instead of solving this problem locally, you can use the GitHub conflict manager (presumably the done thing, avoiding using an IDE)
