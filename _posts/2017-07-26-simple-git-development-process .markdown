---
layout: post
title:  '简单的Git开发流程'
date:   2017-07-26 12:19:46 +0800
categories: git
---

### 个人开发
1. 初始化版本库
- 新建一个文件夹：`mkdir test_git`, 进入文件夹：`cd test_git`
- 初始化版本库：`git init`, 列出所有文件：`ls -a`, 此时会发现test_git文件夹内多了个隐藏目录`.git`(这叫git的版本库, 也叫仓库)

2. 告诉git您的身份
- 名字：`git config user.name xxx`
- 邮箱：`git config user.email xxx@xxx.com`
- 查看设置的名字和邮箱：`git config -e`（实际是test_git/.git/config文件）
- git配置文件默认级别：以上设置均为本地级别，默认`--local`，即`git config user.name xxx => git config --local user.name xxx`
- git配置文件其他级别：`git config --global`(linux下实际是~/.gitconfig)、`git config --system`，其中git优先读取`--local > --global > --system`
- git删除配置文件：例如删除user.name，`git config --unset --local user.name`，值得一提的是删除了`--local`，git会往上找配置，先找`--global`，再找不到到`--system`，连`--system`都没，git还会猜测用户名，例如你操作系统的登录名
- git可以随意设置提交的用户名和邮件地址信息: 这是分布式版本控制系统的特性所决定的，每个人都是自己版本库的主人。团队协作设置一个共享的版本库，在团队成员向共享版本推送新提交时，会进行用户身份认证并检查授权，但不会对提交中的包含的提交者ID作进一步检查

3. 提交第一个版本
- git工作区：在test_git目录下`echo 'init index.html' > index.html`（相当于编辑一个名为index.html的文件，输入init index.html，保存），此操作称为工作区修改
- git暂存区：`git add index.html`（此时把工作区index.html的修改推向暂存区）
- git本地版本库：`git commit -m "add index.html"`（把暂存区的修改推到本地版本库），这些修改将会成为版本历史

4. 分析版本形成过程
- 继续Coding（即工作区修改）: `echo 'add 2nd line' >> index.html`（相当于在index.html内容上编辑下一行，输入add 2nd line，保存）
- 查看当前状态：`git status`可以看到工作区修改的文件名 <font color = 'red'>modified:   index.html</font>
- 查看当前工作区与暂存区差异：`git diff index.html`，此时可以看到：<font color = 'green'>+add 2nd line</font>，说明index.html差异在添加了add 2nd line这行代码
- 提交到暂存区：`git add index.html`
- 查看当前工作区与暂存区差异：`git diff index.html`，此时无任何差异，原因是git add index.html后，已把工作区index.html的修改推向暂存区，所以工作区与暂存区一致
- 查看暂存区与本地版本库差异：`git diff HEAD`，此时可以看到：<font color = 'green'>+add 2nd line</font>
- 暂存区提交到本地版本库：`git commit -m "add 2nd line"`，此时形成一个新的历史，此历史记录了在index.html添加了add 2nd line
- 查看版本历史：我们可以通过`git log`命令查看该版本历史，此时可以发现两个版本，每个版本分别包括commit（40位sha值）、作者信息（git配置的user.name、user.email）、提交时间、提交说明（git commit -m ""填写的内容）

### 如何推向远端库
未完待续...

### 协同开发
未完待续...

#### 推荐参考资料
##### 适合Git新手教程：[廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
##### 适合深入Git的书籍：[Git权威指南](https://book.douban.com/subject/6526452/)

