# git command

# global
    git config --global user.name "pouya pouryaie"
    git config --global user.email "pouyapouryaie@gmail.com"

# add
    git add fileName ('.' that symbol means all file)
    
# reset
    reset index : git rm -r --cached .

# commit

    1- simple : git commit -m "message"
    2- add And Commit : git commit -am "message" (recommend for when you just modify file not added)
    3- commit With IssueDone : git commit -m "message %close #issueNumber" (after that push to remote repo)

# back file to latest station

    1- add file to stage
    2- git reset HEAD
    3- git checkout -- file name

number video seen : 14

# branch command

    add : git branch -b namebranch
    merge : git merge namebranch
    remove after merge : git branch -d namebranch
    create main(master) branch : git branch -M main

# alias

    add command for use with alias name
    ex: git config --global alias.fulllog "log --oneline --graph --decorate --all"
    then in use : git fulllog

# tag

    add : git tag name
    flexibleTag : git tag -a tagName -m "message" commitId
    show detail : git show tagName
    list : git tag --list
    best : git tag -a tagname -m "tag message"
    show comment : git tag -n
    EditTag : git tag -f tagName commitId

# reset

    soft mode : git reset --soft id
    hard mode : git reset --hard id

# revert

    we should only use git revert if we want to apply the inverse of a particular commit. It doesn’t revert to the previous state of a project by removing all subsequent commits, 
    it simply undoes a single commit. git revert doesn’t move ref pointers to the commit that we’re reverting, which is in contrast to other ‘undo’ commands, such as git checkout 
    and git reset. Instead, these commands move the HEAD ref pointer to the specified commit.
    
    command: git revert id

# github

    prepare
    1- first you need create ssh-key : ssh-keygen

    2- copy content in id_rsa-public in github account ssh-key

# push

    1- if you are not repo in local:
        * echo "# gitdemo" >> README.md
        * git init
        * git add README.md
        * git commit -m "first commit"
        * git remote add origin git@github.com:PouyaPouryaie/gitdemo.git
        * git push -u origin master

    2- if you are have repo in local
        * git remote add origin git@github.com:PouyaPouryaie/gitdemo.git
        * if your repo is another server : $ git remote add origin ssh://[serverUser]@[serverIp]:/home/pouya/myrepo
        * git push -u origin master

    3- if you created branch in local and you want push that as new branch in remote repo
        * git push -u origin branchName

    4- if you are push from local in repo anytime
        * git push origin master

    5- if you want use simple push command 
        * git config --global push.default simple
        * git push

    6- if you want send tag to remote repo
        * git push origin tagName
        * git push --tags (send all tags)
    
    7- if you want Edit tag in remote repo
        * git push --force origin tagName
    8- if you want Remove tag from remote repo
        * git push --delete origin tagname

# clone

    git clone repoAddress

# fetch&pull

    pull means fetch from repo and merge with local
        git pull
    for pull specific branch from remote to local
        git pull origin 'branch-name' (recommend before pull in local create branch with same name in remote) 
    
    - if you have 'Git refusing to merge unrelated histories' error you must be add --allow-unrelated-histories to pull request

    pull and rebase on your branch
        git pull --rebase

# rename remote repo in local

    git remote set-url origin newAddress(newName)

# Diff & Show

    - showing for a specific commit
    git show <commit_hash>

    - showing for a specific file
    git show file_name

    -- list of all changes
    git diff-tree -r <commit_hash>

    -- compare two branch -> In short, it will show you all the commits that “branch_2” has that are not in “branch_1”
    git diff <branch_1>..<branch_2>
    
    
# track remote branch on local branch

    git branch --set-upstream-to=origin/<remote-branch> <local-branch>

# Stash

    The git stash command takes your uncommitted changes (both staged and unstaged), saves them away for later use, and then reverts them from your working copy
         - if you create new file and this file have not been staged in git, then when use stash command, this file is ignored by git

    1- basic command: git stash
    2- if you want reapply stage and remove from stash: git stash pop
    3- if you want reapply stage and copy from stash: git stash apply
    4- stash option: 
        - git stash -u : for untrack files
        - git stash -a : for all data, even ignore files
        - git stash list : list of WIP (work in progress) in stash
        - git stash pop/apply stash@{number} : select specific stash
        - git stash save "message" : define description for 
        - git stash show : show diff
        - fir stash show -p : view full diff between files
    5 - Creating a branch from your stash
        - If the changes on your branch diverge from the changes in your stash, you may run into conflicts when popping or applying your stash. Instead, you can use git stash branch to create a new branch to apply your stashed changes to:
            git stash branch add-stylesheet stash@{number}


# branch in remote

    1- first create branch in remote repository
    2- git fetch in local and see created branch in remote repository : git fetch
    3- git checkout remote-branch-name : git checkout remote-branch-name
    4- work on the branch and then commit in local : git commit -am "" (this commit done on the remote-branch-name)
    5- push branch on the remote repository : git push (this change just remote-branch-name)
    6- push branch on the new branch in remote : git push <remote> <local_branch>:<remote_name>

# remove

    branch:
        from local: git branch -d <branchName>
        from remote: git push origin -d <branchName>
    tag:
        from local: git tag -d <tagname>
        from remote: git push --delete origin <tagName>

# rebase

    1- normal:
        git rebase branchName (all of commit in 'branchName' rebase onto current branch)
    2- Interactive:
        git rebase -i branchName (then in file you pick order of commit then save file)
        git rebase -i HEAD~5 (this mean you can rearrange, the last 5 commits)
            # option Commands:
            # p, pick = use commit
            # r, reword = use commit, but edit the commit message
            # e, edit = use commit, but stop for amending
            # s, squash = use commit, but meld into previous commit
            # f, fixup = like "squash", but discard this commit's log message
            # x, exec = run command (the rest of the line) using shell
            # d, drop = remove commit
    3- advance:
        git rebase --onto branchName1 branchName2 branchName3 (we order sequence of branch rebase in one history)
    4- confilict
        * first resolve confilict and then tell git resolve: git add fileName
            ## if you want update index : git rebase --continue
            ## if you skip update : git rebase --skip
            ## if you want undo rebase : git rebase --abort

# change origin and push all-things in new origin

    1. Setup new origin url for local repo
    ```
    git remote set-url origin <yourUrl>
    ```
    2. push all your branch and tags into new repo with one of below command:
    - git push origin '*:*'
    - git push origin --all
    
    
