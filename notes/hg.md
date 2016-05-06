#Hg 笔记

##获取Hg仓库
> * 获取远程代码库的本地拷贝 `hg clone <远程代码库URL路径>`
> * 把本地目录转化为Hg仓库 `hg init`

##把文件加入或剔除版本库管理
> 添加可识别的文件到版本库 `hg add`<br/>
  从版本库中剔除已经被删除的文件 `hg remove`<br/>
  加入可识别的文件，剔除其他文件 `hg addremove`<br/>

> 删除未曾控制的文件 `hg purge`

##查看改动
> * 查看仓库状态(m表示修改过；a表示新加的文件；r要删除的文件；?表示文件状态未知；！丢失的的文件) `hg status`
> * 查看文件/分支修改(加 **-r** 参数指定两个版本进行比较) `hg diff <file/branch>`

##撤销改动
> 撤销修改 `hg revert`
```
hg revert foo               # 放弃对 foo 文件的修改
hg revert -a                # 撤销所有的修改
hg add bar                  # 错误添加了文件 bar
hg revert bar               # 取消添加
hg remove file              # 错误删除了文件 file
hg revert file              # 好的，恢复了
rm file                     # 错了，删错了
hg revert file              # 好的，恢复了
hg copy file newfile        # 错了
hg revert newfile           # 改正就行了
hg rename file newfile      # 错了
hg revert newfile           # 知错就改
hg revert -r 12345 --all    # revert版本12345之后所有的修改，注：版本12345本身的修改不会被revert
```

##把改动写入本地仓库
> 把工作区改动写入本地仓库 `hg commit -m "描述本次修改内容"`<br/>
  指定一个文件写入本地仓库 `hg commit -I <file>`<br/>
  把本次改动追加到上一次改动的本地版本中 `hg commit --amend`

## 废弃和找回一个Commit
> 废弃一个commit `hg strip`
>
> 回滚被strip的commit `hg pull .\.hg\strip-backup\15cb9e0ce79e-backup.hg`

##改动在远程仓库和本地仓库间同步
> 把本地仓库改动推送到远程仓库 `hg push`
>
> **把远程仓库改动同步到本地**<br/>
> 获取远程仓库获取代码库改动 `hg pull`<br/>
  把从远程仓库获取的改动应用到本地工作目录 `hg update`<br/>
  获取代码库的修改的同时更新工作目录 `hg pull -u`<br/>

##查看版本
> 查看代码库Heads `hg heads`<br/>
>
> 查看当前版本 `hg parent`<br/>
>
> 查看所有历史版本 `hg log`

##分支管理
> 新建分支 `hg branch <分支名>`
>
> **查看分支**
> * 当前分支 `hg branch`
> * 所有分支 `hg branches`
>
> **切换分支**
> * 切换分支 `hg update <分支名>`
> * 切换分支的同时，放弃当前分支的改动，不备份 `hg update  -C --clean <分支名>`
> * 切换到指定版本 `hg update <版本号>`
>
> 合并分支 `hg merge <分支名/版本号>`<br/>
> 从其它分支拉取代码并合并 `hg fetch`<br/>
>
> 关闭分支 `hg commit --close-branch -m "close"`


##回滚
> 回滚上一次 Hg 操作 `hg rollback`<br/>
> **注意：**<br/>
> 1.一旦 push 后， rollback 就没用了
> 2. 只能 rollback 一次

##CodeReviewe
> 发送CodeReview `hg postreview`<br/>
  把本次CodeReview发在上次的CodeReview中 `hg postreview -e <上次CodeReview的版本号>`<br/>
  选取一个父节点做为本次CodeReview的Parent `hg postreview --parent <父版本号>`<br/>

##其他
[扩展阅读](http://anotherwayaround.blog.163.com/blog/static/1900662202012326104313552/)
