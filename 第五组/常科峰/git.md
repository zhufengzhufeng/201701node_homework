## pwd
print working directory 打印当前工作目录

## 告诉git当前我是谁
- 用git第一次需要配置，以后不需要，如果不配置则无法提交
```
git config --global user.name github名字  修改或者设置名字
git config --global user.email github邮箱  修改或者设置邮箱
git config --list查看是否配置过名字和邮箱
```
## git init

## 创建文件
- $ touch 文件名

## 查看文件
- $ cat 文件名

## 编辑文件
- $ vi 文件名  ,此时可以编辑内容
- i 插入模式
- ESC      :wq(保存并退出)      q!(不保存退出)

##删除文件夹
- rm -rf 文件名及路径

## 工作区提交到暂存区
- git add .
- git add -A
- git add 文件名

## 暂存区提交到历史区/版本库
- git commit -m "这里写修改日志"

## 文件没有add的文件是红色，没有commit的文件是绿色。
- git status (默认在工作区的文件都是红色，暂存区的是绿色)

## 查看日志
- git log

## 查看代码不同
- git diff (工作区和暂存区区别)
- git diff --cached(暂存区和历史区区别)
- git diff 分支名（工作区和历史区区别）

## 把暂存区的文件覆盖掉工作区文件
- git checkout 文件名

## 把暂存区文件返回到之前的文件
- git reset HEAD .

## 回滚之前的版本
- git log --oneline（先查看线上的版本记录）
- git reset --hard 版本号

## 查看分支
- git branch

## 新建分支
- git branch 分支名

## 切换分支
- git checkout 分支名

## 删除分支
- git branch -D 分支名

## 创建并切换分支
- git checkout -b 分支名

## 合并分支
- git checkout 主分支（先切换到主分支）
- git merge 子分支名
- 如果冲突，修改完后再次提交就可以解决冲突，合并完成。

## echo "readme.md描述" > README.md  重置README.md的内容
## echo "readme.md描述" >> README.md 向README.md追加内容

## 关联仓库
- git remote add 名字 地址

## 推送到远程仓库
- git push origin master -u
- git push(使用条件是在上面命令执行过一次后可以使用此命令推送新的内容到远程仓库)

## 忽略文件
- .gitignore 要忽略的文件需要在add .之前搞定
> git不能提交空文件夹

## 在github上发布静态网站
- 必须在当前项目下建立一个gh-pages的分支
- 将我们需要发布的内容推送到gh-pages这个分支上
- 推送到远程仓库上即可
- github会给你一个在线地址

## 获取自己的仓库代码
- git clone 仓库地址 别名