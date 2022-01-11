# Git Commands Demo
Based on the [Bitwise Standards for git commands](https://github.com/Shift3/standards-and-practices/blob/main/standards/git-commands.md)

## [Learn Git Branching Playground](https://learngitbranching.js.org/?NODEMO)
  * Note some Git commands aren't supported 😢

## **View Status**
---
Frequently used in git terminal to view untracked files, unstaged changes, and currently staged changes.
* `git status`

Used to view commit history
* `git log --oneline`

And some git terminology
* Tracked vs Untracked
  * Git sees new files, but does not know the history of the new files.
    * Files in `.gitignore` are not considered untracked. They are invisible in the eyes of git. 
  * Files that have been staged and committed are tracked
* Staged vs Unstaged
  * Staged files will be included in the next commit
  * Whereas unstaged files will not
* Clean vs Dirty branch
  * Untracked files, tracked files with uncommitted changes denotes a dirty branch
  * Whereas no untracked files, tracked files with all changes committed denotes a clean branch
## **Staging**
---
Before commiting changes, you must stage your changes!
* stage only the specified files
  * `git add <file1> <file2>`...
* stage all modified or deleted files, including untracked files (in vscode, files with a green U)
  * `git add .`

* #### **Cool Feature: Patch**
  Interactively stage selected lines (hunks) in a file
  * `git add -p <file1>` 

Whoops, maybe you accidentally staged the wrong file(s). No worries!
With the latest version of git, there are many ways to unstage file(s)
* remove specified file(s) from staging
  * `git reset -- <file1> <file2>`... or `git reset HEAD <file1> <file2>`...
  * `git restore --staged <file1> <file2>`...
  * `git rm --cached <file1> <file2>`...
* remove all files from staging
  * `git reset` or `git reset HEAD`
  * `git restore --staged .`

## **Commits**
---
After staging any changes, commit your changes!

* `git commit`

Commits changes with the specified message in quotations

* `git commit -m "chore(init): initialize repo"`

  * Going off on a tangent: [Karma Runner commit standard](http://karma-runner.github.io/1.0/dev/git-commit-msg.html)
    * `type(scope): subject`

Automatically stage all modified or deleted files. Untracked files (in vscode, files with a green U) are not staged.

* `git commit -a`

Level up your git terminal skills by combining options!
* `git commit -am "chore(init): initialize repo"`

Luckily for you, git lets you undo commits!
* Or the last commit you made was an accident...
  * Note that there are different ways to undo a commit with different outcomes!
  * Another note, you may see the caret `^` symbol that appends `HEAD` on some commands. This denotes "how many commits before the `HEAD` pointer"
    * So `HEAD^` means "the commit right before `HEAD`"
    * And `HEAD^^` means two commits before `HEAD`
  * `git revert HEAD`
    * Creates and commits an inverse of the last commit. This will undo the last commit but your branch history will have record of both the last commit and the revert commit.
    * **The safest method**. Use this if you're collaborating on a team repo.
  * `git reset HEAD^`
    * Moves the `HEAD` pointer to the previous commit right before the last commit and abandons the last commit.
    * Used in conjuction with `--soft`, `--mixed`, `--hard`
    * **The dangerous method**. [This may cause problems](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset#:~:text=Don%27t%20Reset%20Public%20History) if pushing to a team repo. Only use this if you understand the possible consequences of undoing history and need to undo local changes that have **not ever** been pushed to a remote repo.

## **Branching**
---
List all branches
* `git branch -a`

Create and switch to a new branch using the current branch as a base
* `git branch <new-branch-name>` && `git checkout <new-branch-name>`
* `git checkout -b <new-branch-name>`
* `git switch -c <new-branch-name>`

Rename current branch
* `git branch -m <new-branch-name>

Delete a branch
* Safe delete. Will not delete if unmerged changes exist
  * `git branch -d <branch-name>`
* Force delete. Gotta do what you gotta do
  * `git branch -D <branch-name>`

Merge the current branch with another branch
* `git merge <branch-to-merge>`
## **Code Versioning**
---
Tags are used to easily reference specific commits in Git history 

Create a tag
* `git tag <version-number>`
  * Create a new tag that points to your currently checked out commit
* `git tag <version-number> <commit-SHA>`
  * Create a new tag that points to the specified commit

Delete a tag
* `git tag -d <version-number>`

Tags have to be explicitly pushed to your Github repo
* `git push origin <version-number>`

[Read more about tags here](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-tag)

## Lesser Known Git Commands
---
Some of these commands may require an up to date Git version.
* Scenario 1: You wanna switch from your branch to staging but you cant remember the dang checkout command!
  * `git switch <branch-name>`
  * `git switch -c <new-branch-name>`
    * This will create a new branch and switch to it. Similar to `git checkout -b <new-branch-name`>

* Scenario 2: You were tasked with a bug or feature ticket. You wrote a bunch of spaghetti code that frustrated you so you decide to start fresh from the last commit state and walk away... 😪
  * `git restore <file>`
    * Discard uncommitted changes. Only do this if you wanna erase uncommitted work in progress changes
    * File gets restored to the way it looked in the last commit
* ...Or maybe your last commit is all spaghetti! so you decide lets go back in time!
  * `git restore --source HEAD~1 <file>`
    * Rewind a file back to how it was one commit ago.
    * The restored file is marked as modified. You can make further changes and commit the restored file to keep the rewind
    * ...Or maybe the past isn't so sweet. So you decide back to the future!
      * `git restore <file>` will get you back to where you originally were 
  * [More restore examples here](https://levelup.gitconnected.com/git-restore-a-short-guide-a69d9be343bd)
  
* Scenario 3: Another developer has asked you to review recent changes in another branch, but you are stuck in your current branch with work in progress changes. Your changes are not ready for committing.
  * `git add <files-you-want-stashed>`
    * Stage any files you want stashed
      * Note: Tracked files get stashed whether they are staged or not
      * Unstaged untracked files **do not** get stashed
  * `git stash push`
    * Stash staged changes into a git managed stack called `WIP` (work in progress)
    * Notice your current branch is clean
  * `git stash pop`
    * Apply the last stash stored and remove it from the stack 
  * `git stash list`
    * View stored stashes in the stack
  * [More stash examples here](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning)

* Scenario 4: There are files you no longer need. You delete them but now you have to stage those deleted files before you can commit. Ugh more commands 😪
  * `git rm <file1> <file2>`...
    * A safe way of removing file(s). If the file(s) contain uncommitted changes, git will not remove the file(s)
  * [More rm examples here](https://www.atlassian.com/git/tutorials/undoing-changes/git-rm)