
$git config --global user.name "your name"                //设置你的名字
$git config --global user.email "email@example.com"       //设置你的邮箱

$git init     //让你的目录变成git可以管理的仓库(repository)
$git add <file>   //放到暂存区
$git status
$git commit -m "Operation description"

$git diff <file>  //查看上次是如何修改文件

$git log  //日志  （）
$git log --pretty=oneline

$git reset --hard HEAD^   //回到哪一个版本,  ^上一个版本, ^^上上个版本, HEAD~100 回到100个版本之前
$git reset --hard (num)   //回到未来指定的某个版本

$git reflog              //记录你的每一条命令

$git checkout -- <file>  //丢掉工作区的修改，

$git rm <file>

$ssh-keygen -t rsa -C "youremail@example.com"   //生成id_rsa, id_rsa.pub

$git remote add origin git@github.com:ZhangJun-Mr/learngit.git
 or
$git remote add origin https://github.com/ZhangJun-Mr/gitkills.git

$git push -u origin master (first must use -u)

$git branch   // view all branch
$git branch <name>  //create branch
$git checkout <name>  //switch branch
$git checkout -b <name>  //create and switch branch
$git merge <name>  //Merge from one branch to the current branch
$git branch -d <name>  //delete one branch
$git branch -D <name>  //Mandatory delete one branch

$ git merge --no-ff -m "merge with no-ff" dev    //merging branches
$ git log --graph --pretty=noeline --abbrev-commit  //Check the branch history

$git stash                //storage branch
$git stash apply
$git stach pop
$git stach apply stach@{number}
