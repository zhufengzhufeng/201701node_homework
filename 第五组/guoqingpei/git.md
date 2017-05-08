# git
## pwd
  print working directory 打印当前工作目录

## 告诉git当前我是谁
-- 用git第一次需要配置 以后都不需要，如果不配置则不能提交代码
-- git config --global user.name <github名字>
-- git config --global user.email <github邮箱>
-- git config --list 查看配置列表

## 初始化文件夹 （告诉git那个文件夹归git管理）
-- git init
## cd
-- change directory
## mkdir
-- make directory
## 不能仓库套仓库
-- 不能再初始化后的仓库下，在新建文件夹初始化仓库
查看文件中的内容
-- ls -a

## 删除文件夹
-- rm -rf .git
## 删除文件
-- rm

## 创建文件
-- touch
## 查看文件内容
-- cat

## vi 编辑  不能编辑文件夹 只能编辑文件
-- vi
-- i 插入模式
--ESC  :wq 保存并退出
--q! 强制退出

## 添加暂存区
git add .
git add -A
git add 文件名

## 添加历史区
-- git commit -m "message"

## 查看版本
-- git log
## 代码对比
-- 工作区和暂存区  git diff
-- 工作区和历史区  git diff 分支名
-- 暂存区和历史区  git diff --cached

## 从暂存区拿回文件
-- git checkout
## 回滚某个版本号  从历史区拿回文件（回滚操作 ：在历史区直接找一个版本覆盖掉工作区和暂存区 ）
--  git reset --hard 版本号

## 查看所有历史
-- git reflog
## 搜索
-- git log --grep="搜索字符串"
## 删除本次的add  (加入暂存区后，返回上一次的添加)
-- git reset HEAD 文件名
## 查看当前项目下的分支
-- git branch
## 创建分支
-- git branch dev
## 切换分支
-- git checkout dev
## 删除分支
-- git branch -D dev
## 创建并切换分支
-- git checkout -b dev
## 合并分支
-- 默认master是主干，用主干合并分支
-- 在主干下 git merge dev
>合并分支后 被合并的分支删除即可
## 处理冲突
由于两分支改变了相同的文件，但是内容不同这时候要手动处理，再次提交，就可以完成合并（模块开发可以降低冲突）


## github注册之后需要配置邮箱

## 创建有内容的文件
echo 内容>文件名
echo 内容 >> 文件名（追加内容）
## 关联仓库
-- git remote add 名字 地址
## 推送到远程仓库
--  -u   upstream 你设置后下次推送时可以使用简写
git push origin master -u
git push

## 忽略文件
- .gitignore
要忽略的文件需要在.gitignore建立之后再add
>git 不能提交空文件夹
## 在github上发布静态网站
- 必须当前项目下建立一个gh-pages的分支
- 将我们需要发布的内容推送到gh-pages这个分支上
- 推送到远程仓库上即可
- github会给你一个在线地址

git checkout -b gh-gh-pages
touch index.html
git add .
git commit -m 'add index.html'
在settings中可查找到网址+文件名（默认会展示index.html）

##将文章发送给老师（通过github）









