# Git Basics

A common understanding of how source control works is fundamental to good software engineering hygiene.

## Git vs. GitHub

"Facebook for your code" varying concepts don't exist in raw Git (e.g. pull requests)

## Git Flow

To collaborate more efficiently we can all agree to operate in a specific way. details on Git Flow here.

## Common Commands

 - `git clone`
   - Clone a remote repository to your local machine
 - `git checkout <branch-name>`
   - Switch to the given branch name
   - Use `git checkout -b <branch-name>` to create the branch
 - `git status`
   - Get information about current tracked and untracked files in your local repository
    > Note that untracked files don't belong to any specific branch and changes you made while on one branch can be brought to another branch before tracking
 - `git add <file-name or folder-path>`
   - Add a file or folder to be staged for the current commit
   - Use `git add .` to add all files from your local working directory
   - Use `git add :/ --all` to add all files changed within the repository
 - `git commit`
   - Save the state of the added files
   - Use `git commit -m "<message>"` to add the message for that commit in the same command
 - `git push`
   - Move the file changes saved in your local repository to the remote repository
   - Use `git push --set-upstream <remote-name> <branch-name>` to create your feature branch on the remote repository 
 - `git pull`
   - Get remote file changes and `git merge` them to your local repository
 - `git fetch`
   - Get remote file changes but do not `git merge` them to your local repository
 - `git remote` 
   - Use `git remote -v` for additional verbosity
 - `git revert`
   - Undo the most recent commit
   - Use `git revert --no-commit` to avoid the addition of a revert commit
 - `git reset`
   - Reset the state of the repository to the given hash
   - Use `git reset HEAD --hard` to undo any file changes or additions
   - Use `git reset HEAD --soft` to avoid undoing any file changes or additions
   - Use `git reset HEAD~n` to undo `n` commits prior 
   - Use `git reset <sha>` to undo changes up to a specific commit
 - `git rebase`
   - Change the base commit of your feature branch
 - `git merge <branch-a> <branch-b>`
   - Merge the commits from `branch-a` to `branch-b`
   - `git merge --abort`
   - `git merge --continue`

## Erase a commit on your local repository

## Erase a commit on your remote repository

## Resolve a merge conflict