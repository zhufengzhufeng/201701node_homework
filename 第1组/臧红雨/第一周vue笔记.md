##### pwd
print working directory  打印工作目录

##### 告诉git当前我是谁
- 用git第一次需要配置  以后都不需要
```
git config --global user.name <github名字>
git config --blobal user.email <github 邮箱>
git config --list 查看配置列表
```
##### 初始化文件夹（告诉git哪个文件夹归git所管理）
```
git init
```
##### cd
- change directory

##### mkdir
- make directory

##### 不能仓库套仓库
不能再初始化后的仓库下，在新文件夹初始化仓库

##### 查看文件夹中的内容
```
ls -a
```
##### 删除文件夹
```
rm -rf 文件夹名
```
##### 删除文件
```
rm index.txt
```
##### 创建文件夹
```
mkdir 文件夹的名
```
##### 创建文件
```
touch index.txt
```
##### 查看文件内容
```
cat index.txt
```
##### vi编辑
- 不能编辑文件夹
```
vi index.txt
i 插入模式
ESC   :wq 保存并退出
q!  强制退出
```
从工作区提交到暂存区
```
git add .
git add -A
git add 文件名
```
从暂存区到版本库
```
git commit -m "描述"
```
如果执行过一次增加到版本库
```
git commit -a -m "提交描述"
```

查看状态
```
git status
```
查看版本，日志
```
git log
git log --oneline
git log --grep=作者/日期/内容
git log --graph  查看图谱
```
工作区和暂存区比较不同
```
git diff
```
暂存区和版本区比较不同
```
git diff --cached
```
工作区和版本区比较不同
```
git diff 分支名
```
从暂存区将文件拿到工作区
```
git checkout 文件名
```
从版本区将文件直接找一个版本覆盖掉工作区和暂存区
```
git reset --hard 版本号
```
查看所有的版本号
```
git reflog
```
加入暂存区后返回上一次的添加  删除本次的add
```
git reset HEAD 文件名
```
查看当前项目下的分支
```
git branch
```
创建分支
```
git branch dev(分支名)
```
切换分支
```
git checkout dev
```
删除分支
```
git branch -D dev
```
创建bing切换分支
```
git branch -b dev
```
合并分支
- 默认master是主干
```
git megre dev合并分支名字
```
>分支合并后，被合并的分支删除即可
处理冲突
由于两个分支改变了相同的文件，但是内容不同这时候要手动处理，再次提交，就可以完成合并（模块化开发可以降低冲突）

















