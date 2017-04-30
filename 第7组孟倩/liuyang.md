# git local 命令
## pwd
- 打印当前工作目录

## 告诉git当前我是谁
- 用git第一次时候要配置 以后都不需要，如果不配置不能提交代码
```
git config --global user.name github
git config --global user.email github
git config --list
```

## mkdir
- 创建目录

## cd
- 进入文件夹

## git init
- 初始化文件夹（告诉git哪个文件归他管）
- 注意 不能再Desktop下使用

## 不能仓库套仓库

## rm -rf
- 删除文件夹

## rm
- 删除文件

## ls -a
- 查看文件中的内容

## touch
- 创建文件夹

## cat
- 查看文件夹里面的内容

## vi + 文件名
- 编辑文件， 不能编辑文件夹
- 进去之后按 i 键开始编辑
- 编辑完成后 按Esc键 加：wq（保存并退出）
- q! 强制退出不保存

## git status
- 常看状态在工作区的是红色 暂存区的是绿色

## git add -A || . || 文件名
- 添加暂存区

## git commit -m + 消息
- 添加历史区

## git commit -a -m + 消息
- 直接添加到历史区（前提是中间有一次提交）

## git log
- 查看版本

## git diff
- 比较暂存区和工作区有什么不同

## git diff --cached
- 比较暂存区和历史区有什么不同

## git diff + 分支名
- 比较工作区和历史区有什么不同

## git checkout + 文件名
- 将文件从暂存区拉出来

## git reset --hard + 版本号
- 回滚操作（将文件从历史区拉回来）

## git reflog
- 查看所有的版本

## git log --grep=名字
- 搜索日志

## git log --author=名字
- 搜索用户名字的

## git reset HEAD + 文件名
- 删除当前文件

## history > 1.txt
- 导出一个文件

# git的分支管理

## git branch
- 查看当前有哪些分支

## git branch + 名字
- 创建一个分支

## git checkout + 名字
- 切换分支

## git branch -D + 名字
- 创建并切换分支

#合并分支
- 默认master是主干 用主干合并分支，不是分支合并主干，合并分支后 被合并的分支删除

## git merge
- 需要合并的 分支

#合并分支需要在主干上下达命令

## 处理冲突
- 由于哪个个分支改变的相同的文件，但是内容不同这时候要手动处理，再次提交，就可以完成合并（模块化开发可以降低冲突）

# git remote

## github 注册后需要配置邮箱

## echo 内容 > 文件名
## echo 内容 >> 文件名
- 创建有内容的文件

## git remote add + 名字 地址
- 关联仓库

## git push origin master
- 推送到远程

## .gitignore
- 忽略文件，要忽略的文件需要在.gitignore建立之后再add .
> git 不能提交 空文件夹

## 在github上发布静态网站
- 必须当前项目下建立一个 gh-pages的分支
- 将我们需要发布的内容推送到gh-pages这个分支上
- 推送到远程仓库上即可
- github会给你一个在线地址
```
git checkout -b gh-pages
touch index.html
git add .
git commit -m'add index.html'
git push origin master
在settings中可以查找到网址+文件名即可（默认会展示index.html）
```

# github 团队

## 1
- 组长fork老师
- 组员fork组长

## 2
- 组长克隆自己代码
- 组员也克隆自己代码

## 3
- 组长建立自己组的文件夹，里面放入组员的信息
- 组长提交到自己的仓库

## 4
- 组员和组长建立关系
```
git remote add leader + 组长的地址
```
- 组员拉取组长最新的代码
```
git pull leader master
```
- 将自己写的内容放到文件夹中
- 组员将内容提交到自己的仓库上
- 提交后发送pull request


