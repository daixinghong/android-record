* git add //提交的仓库
* git commit -m “注释” //提交到仓库
* git diff 文件名 //比较文件差别
* git reset -hard HEAD～1 //回退一个版本
* git rm 文件名 //删除文件
* git stash //暂存：如果在开发新的功能时，线上产品有bug，需要新建一个分支，然后保存状态，将原来的分支作为bug分支修改，等解决完  bug后，再将暂存的内容pop出来。
* git remote add //将本地仓库提交到远程库
* git push -u origin master //将本地仓库master分支提交到远程库master分支并关联
* git pull master //同步远程库master分支
* git clone git地址 //将远程库clone到本地
* git checkout -b dev1 //创建新分支dev1，并切换到dev1
* git brach dev1 //创建分支dev1
* git checkout dev1 //切换到dev1分支
* git merge dev1 //合并分支（假如当前分支为master，则时将dev1分支合并到mastr）
* git brach //查看分支
* git brach -d dev1 删除dev1分支
* git cherry-pick 分支合并分支
* git stash pop 把暂存内容拿出来