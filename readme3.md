# git command

# add
    git add fileName ('.' that symbol means all file)

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

# clone

    git clone repoAddress

# fetch&pull

    pull means fetch from repo and merge with local
        git pull
    for pull specific branch from remote to local
        git pull origin 'branch-name' (recommend before pull in local create branch with same name in remote) 

# rename remote repo in local

    git remote set-url origin newAddress(newName)

# show detail in commit

    git show commit id

# branch in remote

    1- first create branch in remote repository
    2- git fetch in local and see created branch in remote repository : git fetch
    3- git checkout remote-branch-name : git checkout remote-branch-name
    4- work on the branch and then commit in local : git commit -am "" (this commit done on the remote-branch-name)
    5- push branch on the remote repository : git push (this change just remote-branch-name)

# remove

    branch:
        from local : git branch -d branchName
        from remote : git push origin :branchName
    tag:
        from remote : git push origin :tagName
        from local : git tag -d tagname

# rebase

    1- normal:
        git rebase branchName (all of commit in 'ranchName' rebase onto current branch)
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