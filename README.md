# Git Commands Demo
Based on the [Bitwise Standards for git commands](https://github.com/Shift3/standards-and-practices/blob/main/standards/git-commands.md)

## **Add these useful commands to your toolbelt**
```
git status
git restore <file>

```
## **Staging**
Before commiting changes, you must stage your changes!

* `git add <file1> <file2> ...`
  * stage only the specified files listed
* `git add .`
  * stage all modified or deleted files, including untracked files (in vscode, files with a green U)

* ### **Options**
        -p --patch
  * stage specified chunks in a file

Whoops, maybe you accidentally staged the wrong file. No worries!

* `git reset -- <file1> <file2>`
  * remove only the specified files listed

* `git reset`
  * remove all files from staging

## **Commits**
After staging any changes, commit your changes!

* `git commit`

```### **Options**
-m "type(scope): subject"
```

Commits changes with the specified message in quotations

* `git commit -m "chore(init): initialize repo"`

  * Going off on a tangent: [Karma Runner commit standard](http://karma-runner.github.io/1.0/dev/git-commit-msg.html)
```
-a --all
```
Automatically stages all modified or deleted files. Untracked files (in vscode, files with a green U) are not staged.

* `git commit -a`
```
-am
```
Level up your git terminal skills by combining options!
* `git commit -am "chore(init): initialize repo"`
## **Branching**
branching stuff goes here
## **Undo Commits and History**
Luckily for you, git lets you undo commits and even go back in time 


## **Code Versioning**