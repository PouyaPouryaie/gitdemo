# Git Commands Tutorial
This repository provides a comprehensive guide to common Git commands, covering essential tasks for version control and collaboration.

# Basic Commands:

## Init
Creating a new Git repository
```bash
git init
```

## Clone
Cloning an existing repository
```bash
git clone <repository-url-address>
```

## Add
Adding files to the staging area
```bash
git add <file-name> or ('.' that means all files)
```

## Commit
Committing changes to the local repository

- simple: `git commit -m "commit message"`
- add & commit: `git commit -am "commit message"`(recommend for when you just modify file not added)
- commit with issue done: `git commit -m "commit message %close #issueNumber"` (after that push to remote repo)
- amend: adding latest changes to the previous commit: 
    `git commit --amend -m "an updated commit message"`

## Status
Checking the current status of the repository
```bash
git status
```
## Log
Viewing the commit history
- showing comprehensive log: `git log <options> <revision-range>`
- Showing compact log: `git log --oneline`
- Showing logs in graph mode: `git log --graph`

## Diff & Show
Comparing changes between commits

- showing for a specific commit
```bash
git show <commit_hash>
```
- showing for a specific file
```bash
git show file_name
```
- list of all changes
```bash
git diff-tree -r <commit_hash>
```
- compare two branch -> In short, it will show you all the commits that “branch_2” has that are not in “branch_1”
```bash
git diff <branch_1>..<branch_2>
```

# Branching and Merging

## Branch
Creating and listing branches

- add new branch: `git branch -b <branch-name>`
- remove a branch: `git branch -d <branch-name>`
- remote a branch for origin: `git push origin -d <branch-name>`
- create main branch : `git branch -M main`
- show list of branch: `git branch -a`

## Checkout
Switching between branches
```bash
git checkout <branch-name>
```

## Merge
Merging branches
```bash
git merge <branch-name>
```

## Rebase
Reordering commits on a branch

- normal:
```bash
git rebase <branch-name> (all of commits in 'branch-name' rebase onto the current branch)
```
- interactive:
```bash
git rebase -i <branch-name> (then in the file you pick the order of commit then save the file)
git rebase -i HEAD~5 (this mean you can rearrange, the last 5 commits)
    # option Commands:
    # p, pick = use commit
    # r, reword = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    # s, squash = use commit, but meld into the previous commit
    # f, fixup = like "squash", but discard this commit's log message
    # x, exec = run command (the rest of the line) using shell
    # d, drop = remove commit
```
- advance:
```bash
git rebase --onto <branch-name-1> <branch-name-2> <branch-name-3> (we order sequence of branch rebase in one history)
```
- conflict: first resolve the conflict and then tell Git to resolve the problem:
```bash 
git add <file-name>
git commit m <commit-message>
# then
# if you want update index: 
git rebase --continue
# if you skip update: 
git rebase --skip
# if you want undo rebase: 
git rebase --abort
```

## Cherry pick
git cherry-pick is a powerful command that enables arbitrary Git commits to be picked by reference and appended to the current working HEAD.<br> Cherry picking is the act of picking a commit from a branch and applying it to another.
- UseCases
    - when a bug is dicovered through developing a new feature and you want to directly commit it to the `main`
    - during team collaboration
    - for merge confilict resolution
        - steps:
            - `git merge --abort`
            - `git log dev` (to find the commit hash)
            - `git cherry-pick <commit-hash>`
            - if you got error:
                - fix the confilict
                - `git add .` or `git add <file>`
                - `git commit -m "commit message"`

```bash
git cherry-pick <commit-hash>
# Steps
1. Find hash-key from `git log`
2. Checkout to the main branch
3. Use cherry-pick command to pick and commit it to main branch
```
- Options
    - `--edit`: will cause git to prompt for a commit message before applying the cherry-pick operation
    - `--no-commit`: will execute the cherry pick but instead of making a new commit it will move the contents of the target commit into the working directory of the current branch.
    - `--signoff`: will add a 'signoff' signature line to the end of the cherry-pick commit message


# Remote Repositories

## Remote
Adding and listing remote repositories
- adding remote repository url: `git remote add origin <remote-url-address>`
- checking remote url:`git remote -v`  

## Push
Pushing commits to a remote repository

- basic command: `git push origin main`
- push a branch to remote: `git psuh origin <branch-name>:<branch-name>`

## Pull
Pulling changes from a remote repository

- basic command: `git pull`

## Fetch
Fetching changes from a remote repository without merging

- basic command: `git fetch`

# Other Useful Commands

## Reset
Resetting the current branch to a specific commit
```bash
# basic
git reset HEAD
# soft mode: 
git reset --soft <commit-id>
# hard mode
git reset --hard <commit-id>
```

## Revert
Reversing a commit

we should only use git revert if we want to apply the inverse of a particular commit. It doesn’t revert to the previous state of a project by removing all subsequent commits, 
it simply undoes a single commit. git revert doesn’t move ref pointers to the commit that we’re reverting, which is in contrast to other ‘undo’ commands, such as git checkout 
and git reset. Instead, these commands move the HEAD ref pointer to the specified commit.
    
`git revert <commit-id>`

## Stash
Temporarily saving changes

The git stash command takes your uncommitted changes (both staged and unstaged), saves them away for later use, and then reverts them from your working copy
    - if you create new file and this file have not been staged in git, then when use stash command, this file is ignored by git

- basic command: `git stash`
- if you want reapply stage and remove from stash: `git stash pop`
- if you want reapply stage and copy from stash: `git stash apply`
- stash options: 
    - `git stash -u` : for untrack files
    - `git stash -a` : for all data, even ignore files
    - `git stash list` : list of WIP (work in progress) in stash
    - `git stash pop/apply stash@{number}` : select specific stash
    - `git stash save "message"` : define description for 
    - `git stash show` : show diff
    - `stash show -p` : view full diff between files
- Creating a branch from your stash
    - If the changes on your branch diverge from the changes in your stash, you may run into conflicts when popping or applying your stash. Instead, you can use git stash branch to create a new branch to apply your stashed changes to:
        - `git stash branch add-stylesheet stash@{number}`

## Tag
Creating tags for specific commits

- add : `git tag <tag-name>`
flexibleTag : `git tag -a <tag-name> -m "message" <commit-id>`
- show detail : `git show <tag-name>`
- list : `git tag --list`
- best-practice : `git tag -a <tag-name> -m "tag message"`
- show comment : `git tag -n`
- editTag : `git tag -f <tag-name> <commit-id>`
- push all new tags: `git push --tags`

## Bisect
    The Git Bisect command performs a binary search to detect the commit that introduced a bug or regression in the project’s history
    1. start the bisect -> git bisect start
    2. define bad commit -> git bisect bad (current branch)
    3. define good commit -> git bisect good <commit_hash>
    4. then bisect starts to move between commits in the range of bad and good commits to find the commit which is a bug introduced there.
    5. after finding the bug, stop the bisect -> git bisect reset
    6. then you can check that commit and revert or fix it with a new commit.
    7. [Tutorial for Bisect] (https://www.youtube.com/watch?v=D7JJnLFOn4A&t=367s)

## Global Config
```bash
git config --global user.name "pouya pouryaie"
git config --global user.email "pouyapouryaie@gmail.com"

# change default branch name while creating new git repository
git config --global init.defaultBranch main
```
    
# Reset Index
`reset index : git rm -r --cached .`


# Some Common Process

## back file to latest station

1. add file to stage
2. git reset HEAD
3. git checkout -- file name

## alias

add command for use with alias name <br>
ex: `git config --global alias.fulllog "log --oneline --graph --decorate --all"` <br>
then in use: `git fulllog`

## github
How to push or pull on a repository at github
1. first you need create ssh-key : ssh-keygen
2. copy content in id_rsa-public in github account ssh-key

### push scenario oh Github

1. if you are not repo in local:
    * echo "# gitdemo" >> README.md
    * git init
    * git add README.md
    * git commit -m "first commit"
    * git remote add origin git@github.com:PouyaPouryaie/gitdemo.git
    * git push -u origin master

2. if you are have repo in local
    * git remote add origin git@github.com:PouyaPouryaie/gitdemo.git
    * if your repo is another server : $ git remote add origin ssh://[serverUser]@[serverIp]:/home/pouya/myrepo
    * git push -u origin master

3. if you created branch in local and you want push that as new branch in remote repo
    * git push -u origin branchName

4. if you are push from local in repo anytime
    * git push origin master

5. if you want use simple push command 
    * git config --global push.default simple
    * git push

6. if you want send tag to remote repo
    * git push origin tagName
    * git push --tags (send all tags)

7. if you want Edit tag in remote repo
    * git push --force origin tagName
8. if you want Remove tag from remote repo
    * git push --delete origin tagname

# fetch & pull

- for pull specific branch from remote to local <br>
`git pull origin <branch-name> (recommend before pull in local create branch with same name in remote)`
    
- if you have 'Git refusing to merge unrelated histories' error you must be add `--allow-unrelated-histories` to pull request

- pull and rebase on your branch
`git pull --rebase`

## rename remote repo in local
```bash
git remote set-url origin newAddress(newName)
```
    
## track remote branch on local branch
```bash
git branch --set-upstream-to=origin/<remote-branch> <local-branch>
```

## How to create a branch in remote and use it

1. first create a branch in remote repository
2. fetch in local repo and see the list of branch in remote repository: `git fetch`
3. checkout the branch on your local: `git checkout <branch-name>`
4. work on the branch and then commit in local: `git commit -am "" (this commit done on the branch-name)`
5. push branch on the remote repository: `git push`
6. push branch on the new branch in remote: `git push <remote> <local-branch-name>:<remote-branch-name>`

## some remove scenario

- branch:
    - from local: `git branch -d <branchName>`
    - from remote: `git push origin -d <branchName>`
- tag:
    - from local: `git tag -d <tagname>`
    - from remote: `git push --delete origin <tagName>`


## change origin and push all-things in new origin

1. Setup new origin url for local repo
```bash
git remote set-url origin <new-url>
```
2. push all your branch and tags into new repo with one of below command:
```bash
git push origin '*:*'
git push origin --all
```
