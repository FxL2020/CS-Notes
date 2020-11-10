### Git 结构
工作区--git add-->暂存区-->git commit-->git库
### Git 和代码托管中心
代码托管中心的任务：维护远程库
局域网环境下
GitLab 服务器
外网环境下
GitHub
码云
### 本地库和远程库
团队内部协作
员工1 --从远程库--clone克隆-->本地库1--push-->远程库 --员工2-->pull-本地库2->push--远程库
跨团队协作
远程库1--fork->远程库2-->clone-本地库2-push--远程库2-->pull request--审核--merge--远程库1--pull--本地库1
### Git 命令行操作
#### 本地库初始化
```shell
mkdir chat //创建项目
git init   //初始化 生成了.git文件
ll .git/
```
#### 设置签名
形式
用户名：tom
Email地址：222@ty.com
作用：区分不同开发人员的身份
命令：
项目级别/仓库级别：仅在当前本地库范围内有效
```shell
git config user.name tom_pro
git config user.email goodMorning_pro@atguigu.com
信息保存位置：./.git/config 文件
```
系统用户级别：登录当前操作系统的用户范围
```shell
git config --global user.name tom_glb
git config --global user.email goodMorning_pro@atguigu.com
信息保存位置：~/.gitconfig 文件
```
就近原则：项目级别优先于系统用户级别，如果只有系统用户级别的签名，就以系统用户级别的签名为准，二者都没有不允许
### 基本操作
#### 状态查看
查看工作区、暂存区状态
```shell
git status
```
添加
将工作区的“新建/修改”添加到暂存区
```shell
git add file
```
提交
将暂存区的内容提交到本地库 -m 带上提交说明信息
```shell
git commit -m "my first commit" [filename]
```
#### 查看历史记录
```shell
git log   //显示太详细
git log --pretty=oneline  //显示简洁些
git log --oneline
git reflog  //HEAD@{移动到当前版本需要多少步}
```
多屏显示控制方式：
空格向下翻页
b 向上翻页
q 退出
#### 历史版本前进后退
基于索引值操作[推荐]
```shell
git reset --hard [局部索引值]
git reset --hard a6ace91
```
使用^符号：只能后退
```shell
git reset --hard HEAD^^  注：一个^表示后退一步，n 个表示后退 n 步
```
使用~符号：只能后退
```shell
git reset --hard HEAD~n //注：表示后退 n 步1 2 3..
```
#### 删除文件并找到
前提：删除前，文件存在时的状态提交到了本地库。
```shell
操作：git reset --hard [指针位置]
```
删除操作已经提交到本地库：指针位置指向历史记录
删除操作尚未提交到本地库：指针位置使用 HEAD
#### 比较文件差异
比较文件差异
git diff [文件名]
将工作区中的文件和暂存区进行比较
git diff [本地库中历史版本] [文件名]
将工作区中的文件和本地库历史记录比较
不带文件名比较多个文件
### 分支管理
#### 什么是分支
在版本控制过程中，使用多条线同时推进多个任务
```shell
 热修复分支                                         |hot_fix------|
file                     master----- -   | ------|      --------  |-------|-------------
file 复制1份       feature_biue-- |                                          |
file 复制2份     feature_game--------------------------------|
```
#### 分支的好处
同时并行推进多个功能开发，提高开发效率
各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任
何影响。失败的分支删除重新开始即可
#### 分支操作
查看所有分支
```shell
git branch -v
git branch -al //查看本地和远程的所有分支。
这样就可以看到所有的分支，
其中master是本地分支，
前面的星号*表示正在使用的分支
前面带有remotes的分支都是远程分支
```
创建分支
```shell
git branch hot-fix(分支名)
```
切换分支
```shell
git checkout hot_fix(分支名)
```
合并分支
切换到被合并的分支上
```shell
git checkout 被合并分支名
git merge hot-fix  //把hot_fix那个分支合并到被合并分支上
```
git pull
：取回远程主机某个分支的更新，再与本地的指定分支合并
```shell
git pull = git fetch + git merge
```
git fetch不会进行合并执行后需要手动执行git merge合并分支，而git pull拉取远程分之后直接与本地分支进行合并。更准确地说，git pull使用给定的参数运行git fetch，并调用git merge将检索到的分支头合并到当前分支中。
```shell
git pull <远程主机名> <远程分支名>:<本地分支名>
git pull origin master:brantest
git pull origin master //与当前分支合并

git fetch origin master:brantest 
git merge brantest
```
git fetch更安全一些，因为在merge前，我们可以查看更新情况，然后再决定是否合并






解决冲突
冲突的解决
 第一步：编辑文件，删除特殊符号
第二步：把文件修改到满意的程度，保存退出
第三步：git add [文件名]
第四步：git commit -m "日志信息"  注意：此时 commit 一定不能带具体文件名

### Git 保存版本的机制
集中式版本控制工具的文件管理机制
以文件变更列表的方式存储信息
Git 的文件管理机制
Git 把数据看作是小型文件系统的一组快照。每次提交更新时 Git 都会对当前
的全部文件制作一个快照并保存这个快照的索引。为了高效，如果文件没有修改，
Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。所以 Git 的
工作方式可以称之为快照流。
### 创建远程库
库名和本地库一样
创建远程库地址别名
```shell
git remote -v   //查看当前所有远程地址别名
git remote add 别名  远程地址
```
https://blog.csdn.net/xqhys/article/details/98113227
git add . 添加全部已经修改的文件，准备commit 提交 
该命令效果等同于 git add -A
#### 推送
```shell
git push 别名 分支名
```
#### 克隆
新键一个本地仓库
```shell
git clone 
```
效果
完整的把远程库下载到本地
创建 origin 远程地址别名
初始化本地库








从暂存区撤销到工作区
git rm --cached good.txt
window 10 凭据
想切换别的账号可以清除掉



