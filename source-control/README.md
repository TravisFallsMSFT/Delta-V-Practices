# Git Basics

A common understanding of how source control works is fundamental to good software engineering hygiene.

## Git vs. GitHub

"Facebook for your code" varying concepts don't exist in raw Git (e.g. pull requests)

## Plumbing
Ideally the way we get started on a project is to setup all the "plumbing" as early as possible. If we expect a solution to exist in a Docker container, for example, this container should be added with a simple "Hello World" application first to ensure that this works.

## Git Flow

To collaborate more efficiently we can all agree to operate in a specific way. Adopting Git Flow 

Steps
 - Pull `main` and `dev` to ensure you have the latest
 - Create a new branch from `dev`
   - Name this branch with your initials or alias, slash, then what you're working on
   - e.g. `je/api-script`
 - Add requirements of the given feature
 - Write appropriate unit tests to ensure those requirements are met
 - Write integration tests to ensure your code does not break the repository
 - Create a pull request on GitHub with 2 or more reviewers
 - Once all issues are rectified, conflicts are resolved, and CI/CD tests pass, the branch can be merged

## Pull Requests

 - All pull requests should be merged or closed by the end of the sprint
 - Pull requests should represent concise units of a task or feature and be kept small in size

## Branch Protection

 - Disable push to main 
 - Only dev can PR into main
 - All feature branches come off of dev
 - All code that is PR'd contains unit and integration testing

## Code Review Tips

Code reviews present an opportunity for sharing and growth. Remember that code reviews should always remain **entirely impersonal**. Remove the person from your feedback, and as a developer know that you are not your code. Much context around body language and tone of voice is lost over text so be sure to always provide code reviews that focus on only the quality of the code and potential risks. Likewise, do not interpret others reviewing your code as anything but helpful and productive. 

Questions that may help guide you during the code review process

 - Is this section of the code the part that is responsible for this feature?
 - Does the developer need to see this here or can/should it be abstracted away?
 - Does this code make assumptions about what is given to it or taken from it?
 - Does the code introduce unnecessary complexity?
 - Is this a solved problem?
 - Is the code repetitive?
 - Does

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
   - Use `git revert --no-commit` to avoid "merge conflict" the addition of a revert commit
 - `git reset`
   - Reset the state of the repository to the given hash
   - Use `git reset HEAD --hard` to undo any file changes or additions
   - Use `git reset HEAD --soft` to avoid undoing any file changes or additions
   - Use `git reset HEAD~n` to undo `n` commits prior 
   - Use `git reset <sha>` to undo changes up to a specific commit
 - `git rebase`
   - Change the base commit of your feature branch
 - `git merge <other-branch>`
   - Merge the commits from a branch into the branch you are currently on 
   - Use `git merge --abort` to abandon the merge and undo any changes 
   - Use `git merge --continue` to indicate that you have resolved any merge conflicts
 - `git branch`
   - List all local branches
   - Use `git branch -D <branch-name>` to delete a branch
  
## Erase a commit on your local repository

If you committed changes to the repository and later realized you wanted to undo that commit, you can easily reset your local repository so that the commit no longer appears. Note that the file changes still exist because we use the `--soft` argument.

```
git reset HEAD~1 --soft
```

## Erase a commit on your remote repository

If you committed changes that you pushed to the remote but you'd like to undo that work, you can do so using a force push. First, undo the commit locally. Note that the changes made to these files no longer exist as we've used the `--hard` argument.

```
git reset HEAD~1 --hard
```

Once you have reset locally you can make different changes if necessary. After you've committed these changes you would perform a force push to rewrite the commit history on your remote repository

```
git push --force
```

## Redo an action
In addition to the above methods of undoing changes you've made, you can also go forward in time by redoing changes you've erased. `git` keeps a `reflog` of all commands you've executed, so you're able to point to those commands and reset to the state prior to execution using 

```
git reset HEAD@{1}
```

## Resolve a merge conflict
When two branches have differing, overlapping file changes, performing a `git merge` will result in a merge conflict. A merge conflict writes directly to the file where it arose and indicates the changes on your branch as well as the changes on the base branch.

```
file.md

<<<<<<< <HEAD of base branch> 
I think abc
=======
I definitely think xyz
>>>>>>> <Your most recent commit sha>
```

To resolve a merge conflict you must consolidate the state of the file. This means deciding if you want to keep your changes, the base branch changes, or a combination of the two.

```
file.md

I definitely think abc
```

Once the file is in a valid state again and you've removed the indicators created from the merge conflict you can use `git merge --continue` to add the changed file.