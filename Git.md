Git是一个版本控制工具，分布式版本控制系统（文件都在本地电脑上），元数据方式存储，内容完整性更优。

它的作用是把项目进度以树形结构呈现，而不是传统的链式结构，方便修改，存储项目。功能有：协同修改，数据备份，版本管理，权限控制，历史记录，分支管理等。。（如果sai2也有这个功能就好了）

优势：大多数操作不需要联网，完整性，方便，删除和修改被精简。

组成：工作区，暂存区，本地库.git，远程库

### 一般操作（白话）

add添加，commit上传，push推送，clone克隆，fork复刻（艹这原来是音译）pull request拉取请求，merge合并

通过git add从工作区添加到暂存区，通过git commit从暂存区提交到本地库。

（团队内部）本地库push到远程库，远程库clone到本地库，本地库加入团队之后才能push到远程库。

（跨团队）远程库甲fork到远程库乙，远程库乙修改之后再pull request，审核通过之后就可以merge，就可以利用本地库甲pull到本地库了。

### 命令行操作,统一前缀都是git

是基于linux的。

cd进入文件夹，ll查看目录，前面加点的隐藏文件，

git add

.git目录中存放的是本地库相关的子目录和文件

设置签名（用户名和Email地址），用来区分开发人员，和github的账号密码没有关系。

项目级别仅在本地库范围内有效

```c++
git config user.name [your name]
git config user.email [your email]
信息保存位置.git/config
```
系统用户级别的范围是登录当前操作系统的用户范围，要有一个签名才能进行操作
```c++
git config --global user.name [your name]
git config --global user.email [your email]
git status//查看工作区和暂存区的状态
git add [file name]//将工作区的新建文件，修改文件
git commit -m "commit message" [file name]提交到本地库
git log//查看历史记录
  git log --pretty=oneline//漂亮的单行显示
  git log --oneline
  git log reflog
  前面那串是哈希码
 HEAD指针，寻找历史版本可以基于索引值操作。
```
####  常用的git指令

```c++
 git branch [newBranchName]在枝干这里新建一个branch
 git checkout -b [newBranchName]新建一个branch，然后选中这个分支
 //“分支”的意思似乎没有branch准确
 git switch [branch]HEAD指向branch
```
```plain
 git checkout [branch]令HEAD选中这个branch
             -B 强制覆盖掉那些同名的branch
git commit 把选中的branch，“伸展”出一个分支
git merge [fixCode] fix合并到master里面，master是最新的，父节点是fix和master之前所在的节点
git rebase [master] 将fix放置于master的前面，fix是最新的，父节点是master
master^    master的父节点
master~n    master的（n个父）节点
git branch -f [branch] [destination]使得branch指向destination
git reset HEAD~1 将HEAD指向的本地branch，ctrl+z
git revert [branch] 将HEAD指向的远程 branch，ctrl+z，保存撤销记录
```
git cherry-pick 一串节点
git rebase -i [node]以node为分支起点，将当前节点栈式存储

git rebase node1 node2 将node2移动到node1这里

git tag [tag][node]给node取tag名

git fetch复制过去，git pull = git fetch + git merge

### GitHub

它是一个结合了云盘，社交，协同工作功能的网站

git remote add origin git@github.com:name/learngit.git

git push -u origin master//这样就可以把本地commit的.git文件上传到github的仓库

git clone git @github.om:xiranqianqing/gitskills.git

这样可以把xiranqianqing的gitskills从仓库复制到本地库

git的分支只会改变指针，不消耗性能和网络，多创建也没关系。

