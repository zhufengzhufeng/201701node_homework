## Git

##### 基本流程
- 1.配置用户名和邮箱
	-  用git第一次需要配置， 以后都不需要

```
	git config --global user.name <github用户名>
	git config --global user.email  <邮箱>
	git config --list 			//查看配置列表
```
- 2.初始化文件夹为git版本库

```
	git init
	rm -rf .git								撤销仓库
```

**注意：不能嵌套初始化**

-  3.工作区提交到暂存区
```
	git add .
	git add -A
	git add 文件名           
```

- 4.暂存区提交到版本区
	`git commit -m"提交说明"`
	 - 查看状态
	`git status`
	 - 查看历史版本信息
	`git log`
	`git log --oneline` 查看缩略的历史ID
	`git reflog`             查看所有版本信息
	`git log --grep=<文件内容>`      条件查询
	`git log --author(作者)=chengxiao`   
- 5.比对文件
```
	git diff                默认对比工作区和暂存区
	git diff --cached       对比暂存区和版本区
	git diff <分支号>        对比工作区和版本区某个分支
```
- 6.暂存区撤销到工作区
```
	git checkout <文件名>
	git checkout .
```
- 7.回滚
```
   git reset <版本号>          版本区的某个版本覆盖暂存区
   git reset --hard <版本号>   版本区直接找一个版本覆盖掉工作区和暂存区
   git reset HEAD <文件名>/.     版本区上一个版本覆盖暂存区
```
- 8.工作区直接添加到暂存区并且添加到版本区
 `git commit -a -m#`
##### 分支
- 1.`git branch dev`       创建分支dev
- 2.`git checkout dev`  切换到分支dev
- 3.`git checkout -b dev` 创建并切换到分支dev
- 4.`git branch`               查看所有分支
- 5.`git branch -D dev`   删除分支dev
 **注意：如果在master中未提交过就创建并切换到dev分支，那么master会丢失**
 **更改提交之前如果切换分支，则会丢失**
- 6.`git merge <分支名>`   合并分支（默认master是主干，用主干合并分支）
 **注意：处理冲突（不同分支改变了同一文件）：手动保留一份**
 
#####  远程git
1.`git remote add <关联名字> <地址>`  关联远程库
2.`git push origin master -u`        本地版本库推送到远程
设置一次-u，后面只需要`git push`
3.`git remote rm origin`                删除关联origin
- .gitignore    要忽略的文件需要在.gitignore建立之后再add
> git不能提交空文件夹
>  必须当前项目下建立一个gh-pages的分支
>  将我们需要发布的内容推送到gh-pages这个分支上
>  推送到远程仓库即可
> github会给你一个在线地址

```
	git checkout -b gh-pages
	touch index.html
	git add .
	git commit -m"add index.html"
	git push origin gh-pages
	在settings中可查找到网址+ 文件名即可（默认展示index.html）
```

获取自己仓库的代码
  `git clone https://github.com/GayeChen/201701node_homework`
