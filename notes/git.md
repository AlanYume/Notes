#Git 笔记

##安装
###Linux 版本
> * 命令行安装 `sudo apt-get install git`
> * **源码安装**<br/>
        1. `./config`<br/>
        2. `make`<br/>
        3. `sudo make install`<br/>

###Mac OS X
> 从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads
”，选择“Command Line Tools”，点“Install”就可以完成安装了。
![MAC OS X 安装 git](http://www.liaoxuefeng.com/files/attachments/001384907061183ba2a452af9de4a8a8640339239bc3e5e000/0)

### Windows 版本
> 1. 从<https://git-for-windows.github.io>下载
> 2. 按默认选项安装
> 3. 开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功
     ![Git 窗口](http://www.liaoxuefeng.com/files/attachments/001384907073134ef6feff559cf4ce3a2c5c588d2831c0a000/0)

## 设置全局用户名与邮箱
> `git config --global user.name "Your Name"`<br>
   `git config --global user.email "email@example.com"`<br/>

## 版本管理
1.  创建Git 仓库
    > 创建空目录 `mkdir learngit`<br/>
      进入该目录 `cd learngit`<br/>
      把目录转化为Git仓库 `git init`<br/>
2.  把改动写入仓库
    > [有关工作区、暂存区、版本库的介绍](http://www.worldhello.net/2010/11/30/2166.html)<br/>
      查看仓库状态 `git status`<br/>
      查看改动内容 `git diff`<br/>
      把工作区改动写入暂存区 `git add <file>`<br/>
      把暂存区内容存入版本库 `git commit -m "本次改动的信息"`<br/>
3.  在改动节点间切换
    > 查看提交历史 `git log`<br/>
      显示精简版的改动历史 `git log --pretty=oneline`<br/>
      显示分支图 `git log --graph`<br/>
      切换到前一个节点(HEAD 表示当前节点) `git reset --hard HEAD^` 或 `git reset --hard HEAD~1` 或 `git reset
--hard <CommitID>`<br/>
      查看命令历史 `git reflog`
4. 撤销修改
    > 丢弃工作区的修改 `git checkout --file`<br/>
       撤销暂存区的修改（用版本库的内容覆盖暂存区）`git reset HEAD file`<br/>
       从版本库中删除文件 `git rm file`<br/>
5. 关联远程仓库
    > 1. 创建 SSH Key<br/>
          在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa
         .pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：`ssh-keygen -t rsa -C
          "youremail@example.com"`，写上你的邮件地址，然后使用默认值一路回车<br/>
    > 2. 如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，**id_rsa**是私钥，不能泄露出去，**id_rsa
        .pub**是公钥
    > 3. 登录GitHub，在**SSH Keys**页面添加**公钥**
          ![添加公钥](http://www.liaoxuefeng.com/files/attachments/001384908342205cc1234dfe1b541ff88b90b44b30360da000/0)
    > 4. 创建远程仓库![创建远程仓库](http://www.liaoxuefeng.com/files/attachments/0013849084639042e9b7d8d927140dba47c13e76fe5f0d6000/0)
    > 5. 把本地仓库关联到远程仓库 `git remote add origin git@github.com:<用户名>/<仓库名>.git`
    > 6. 推送本地仓库的修改到远程仓库的*master*分支 `git push -u origin master`
6. 把远程仓库克隆到本地并自动与远程仓库关联 `git clone git@github.com:<用户名>/<仓库名>.git`
7. 分支管理
    > 查看分支 `git branch`<br/>
    >
    > **切换分支**
    > > * 创建分支 `git branch <分支名>`<br/>
    > > * 切换分支 `git checkout <分支名>`<br/>
    > > * **创建并切换分支** `git checkout -b 分支名`
    >
    > **合并分支**
    > > * 合并分支(快速合并) `git merge <分支名>`<br/>
    > > * 普通合并(合并的同时会有合并节点) `git merge --no-ff <分支名>`
        删除分支(前提该分支已经合并) `git branch -d <分支名>`<br/>
        删除未合并的分支 `git branch -D <分支名>`<br/>
8. 保留现场
    > 存储当前现场 `git stash`<br/>
      查看保存的现场 `git stash list`<br/>
    >
    > **恢复现场**
    > > * 用`git stash apply`恢复，但是恢复后，stash内容并不删除，需要用`git stash drop`来删除
    > > * 恢复的同时删除stash `git stash pop`
    > > * 恢复到指定 stash `git stash apply stash@{0}`
9. 多人协作
    > 1. 查看远程库信息 `git remote -v`<br/>
    > 2. 从本地推送分支 `git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交
    > 3. 本地创建和远程分支对应的分支 `git checkout -b branch-name origin/branch-name`
    > 4. 建立本地分支和远程分支的关联 `git branch --set-upstream branch-name origin/branch-name`
10. 标签管理
    >
    > **查看标签**
    > > 查看所有标签 `git tag`<br/>
        查看指定标签的内容 `git show <tagname>`<br/>
    >
    > **添加标签**
    > > 在当前分支所在commit节点打标签 `git tag <name>`<br/>
        在指定节点打标签 `git tag <标签名> <节点号>`<br/>
        创建带有说明的标签，用-a指定标签名，-m指定说明文字 `git tag -a <标签名> -m "说明" <节点号>`<br/>
    >
    > **删除标签**
    > > * 删除标签 `git tag -d <标签名>`<br/>
    > > * **删除远程仓库标签**<br/>
    > > > 1. 删除本地标签 `git tag -d <标签名>`
    > > > 2. 从远程删除 `git push origin :refs/tags/<1步骤指定的标签名>`
    >
    > **推送标签到远程仓库**
    > > 推送指定标签到远程 `git push origin <tagname>`<br/>
        一次性推送所有标签到远程  `git push origin --tags`<br/>

##自定义
> 显示颜色 `git config --global color.ui true`<br/>
  把不要加入版本管理的文件写入**.gitignore文件**，该文件应位于版本库根目录<br/>
  强制添加文件进仓库 `git add -f <file/directory >`

> 配置别名
```
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.unstage 'reset HEAD'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

> [搭建 Git 服务器](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
/00137583770360579bc4b458f044ce7afed3df579123eca000)

##让Git记住密码

### Linux
```
cd ~
touch .git-credentials
vim .git-credentials
# 将以下内容写入该文件中
https://{username}:{password}@github.com
# 或者
https://{username}:{password}@192.168.0.108

#运行以下git配置命令
git config --global credential.helper store
```
到这一步，执行完后查看Git目录下的.gitconfig文件，会多了一项：
```
[credential]
    helper = store
```
### Windows
1. 在home文件夹，一般是 C:\Users\Administrator 下建立文件 **.git-credentials**文件
2. 输入如下内容 `https://{username}:{password}@github.com`
3. 运行以下git配置命令：`git config --global credential.helper store`
4. 重新打开git bash即可，无需再输入用户名和密码了
