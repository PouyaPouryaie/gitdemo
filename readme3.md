# this is readme3

#for back file to latest station
1- add file to stage
2- git reset HEAD
3- git checkout -- file name

number video seen : 14

#for branch command
add : git branch -b namebranch
merge : git merge namebranch
remove after merge : git branch -d namebranch

#for alias
add command for use with alias name
ex: git config --global alias.fulllog "log --oneline --graph --decorate --all"
then in use : git fulllog

#for tag
add : git tag name
list : git tag --list
delete : git tag -d tagname
best : git tag -a tagname -m "tag message"
