# Git Commands Demo
Based on the [Bitwise Standards for git commands](https://github.com/Shift3/standards-and-practices/blob/main/standards/git-commands.md)

## **Gitflow Basics**
---
### **View Status**
Frequently used in git terminal to view untracked files, unstaged changes, and currently staged changes.
* `git status`

And some git terminology...
* Tracked vs Untracked
  * Git sees new files, but does not know the history of the new files.
    * Files in `.gitignore` are not considered untracked. They are invisible in the eyes of git. 
  * Files that have been staged and committed are tracked
* Staged vs Unstaged
* Clean vs Dirty branch
  * Untracked files, tracked files with uncommitted changes denotes a dirty branch
### **Staging**
Before commiting changes, you must stage your changes!
* stage only the specified files
  * `git add <file1> <file2>`...
* stage all modified or deleted files, including untracked files (in vscode, files with a green U)
  * `git add .`

* #### **Cool Feature: Patch**
  Interactively stage selected lines (hunks) in a file
  * `git add -p <file1>` 

Whoops, maybe you accidentally staged the wrong file(s). No worries!
* remove specified files from staging
  * `git reset -- <file1> <file2>`... or `git reset HEAD <file1> <file2>`...

* remove all files from staging
  * `git reset` or `git reset HEAD`

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
Create a new branch using the current branch as a base
* `git branch <new-branch-name>` && `git checkout <new-branch-name>`
* `git checkout -b <new-branch-name>`
* `git switch -c <new-branch-name>`

Merge the current branch with another branch
* `git merge <branch-to-merge>`

### **Structure**

## **Code Versioning**
---
`git tag`
## Lesser Known Git Commands
---
Some of these commands may require an up to date Git version.
* Scenario 1: You wanna switch from your branch to staging but you cant remember the checkout command!
  * `git switch <branch-name>`
  * `git switch -c <new-branch-name>`
    * This will create a new branch and switch to it. Similar to `git checkout -b <new-branch-name`>
* Scenario 2: There are files you no longer need. You delete them but now you have to stage those deleted files before you can commit. Ugh more commands 😪
  * `git rm <file1> <file2>`...
    * A safe way of removing file(s). If the file(s) contain uncommitted changes, git will not remove the file(s)
  * `git rm --cached <file1> <file2>`...
    * Can also use this command to only remove changes from staging via `--cached`
* Scenario 3: Another developer has asked you to review recent changes in another branch, but you are stuck in your current branch with work in progress changes. Your changes are not ready for committing.
  * `git add <files-you-want-stashed>`
    * Stage any changes you want stashed
  * `git stash push`
    * Push those staged changes into a git managed branch called `WIP` (work in progress)
  * `git stash pop`
* `git cherry-pick`
* `git restore <file> `