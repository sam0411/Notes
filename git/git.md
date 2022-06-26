## Git Reference
http://www.ruanyifeng.com/blog/2014/06/git_remote.html
http://www.ruanyifeng.com/blog/2015/12/git-workflow.html
http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html
http://www.ruanyifeng.com/blog/2015/08/git-use-process.html
http://www.cnblogs.com/cnblogsfans/p/5075073.html
http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/

## GITHUB API
https://api.github.com/users/sam0411  


## Git Commands

## git initialize & push
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:sam0411/test.git
git push -u origin master

## git setup
git config --global user.name "sam0411"
git config --global user.email "sam0411@yeah.net"
git config --global --unset http.proxy
git config --global push.default matching
git config --global color.ui true
git init
git config core.ignorecase false

## ssh key
ssh-keygen -t rsa -C "sam0411@yeah.net"

ssh git@github.com

## add, commit, push | rm | checkout
git add <file name to add to git>
git add -A <file name to add to git>
git rm <file name to remove to git>
git commit -m "commit comments"
git checkout -- <file name to revert>


## branch | checkout | merge
git branch
git branch dev
git checkout dev
git checkout -b dev (create branch and switch to created branch)
git checkout -b dev origin/dev
git branch -d dev
git branch -D dev

## branch | merge
git merge dev (default, Fast-forward model)
git merge --no-ff -m "merge with no-ff" dev


## stash
git stash
git stash list
git stash apply
git stash drop
git stash pop


## status, log, reflog, diff
git status
git log
git log --pretty=oneline
git log --graph
git log --graph --pretty=oneline --abbrev-commit
git reflog
git diff <file name to compare with latest>
git diff HEAD -- <file name to compare with latest>


## reset
git reset --hard HEAD^
git reset --hard HEAD^^
git reset --hard HEAD~100
git reset HEAD <file name to revert>



## tag
git tag
git tag <tag name> -m "tag comments"
git tag <tag name> <sh1 ref>
git tag -d <tag name>
git show <tag name>




## repository
git remote
git remote -v
git remote add origin git@github.com:sam0411/Java_Base.git
git push -u origin master
git push origin <master / branch / tag>
git push origin springboot_2.5.12:springboot_2.5.12     
git branch --set-upstream branch1 origin/branch1
git push origin --delete <branch / tag>
git clone git@github.com:sam0411/Bootstrap3.git