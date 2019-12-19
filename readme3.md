# git command

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
    list : git tag --list
    delete : git tag -d tagname
    best : git tag -a tagname -m "tag message"
    show comment : git tag -n

# reset

    soft mode : git reset --soft id
    hard mode : git reset --hard id

# github

    prepare
    1- first you need create ssh-key : ssh-keygen

    2- copy content in id_rsa-public in github account ssh-key

# push

    1- if you are not repo in local:
        echo "# gitdemo" >> README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin git@github.com:PouyaPouryaie/gitdemo.git
        git push -u origin master

    2- if you are have repo in local
        git remote add origin git@github.com:PouyaPouryaie/gitdemo.git
        git push -u origin master

    3- if you are push from local in repo anytime
        git push origin master

    4- if you want use simple push command 
        git config --global push.default simple
        git push

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

# remove branch

    from local : git branch -d branch-name
    from remote : git push origin :branch-name