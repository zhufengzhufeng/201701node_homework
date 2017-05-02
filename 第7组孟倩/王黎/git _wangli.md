##  git    —第十周 周六

### 版本控制工具
> git 比较快 ，分布式
> svn 保存有一个

```
pwd print working directory 打印当前工作目录
```
### 告诉当前

```
git config  --global user.name github 名字
git config  --global user.name 邮箱
```

### 查看配置列表
```
git config --list
```
### 初始化文件夹（告诉git哪个文件夹归git所管理）
```
git init
```
### cd 
- change directory

### mkdir 
- make directory

### 不能仓库套仓库
不能再初始化后的仓库下，在新建文件夹初始化仓库

### 查看文件中的内容
```
ls -a
```
### 删除文件夹
```
rm -rf .git
```
### 删除文件
```
rm index.txt
```
### 创建文件
```
touch index.txt
```

### 查看文件内容
```
cat index.txt
```

### vi编辑
- 不能编辑文件夹
```
vi index.txt
i 插入模式
ESC :wq保存并退出
q! 强制退出
```

### 添加暂存区
```
git add .
git add -A
git add 文件名
```

### 添加历史区
```
git commit -m '消息'
```

### 查看版本 
```
git log
```

### 代码对比
- 工作区和暂存区
```
git diff
```
- 工作区和历史区
```
git diff 分支名
```
- 暂存区和历史区
```
git diff --cached
```

> 如果执行过一次增加到版本库 git commit -a -m"write hello"

### 回滚某个版本
```
git reset --hard 版本号
```

### 查看所有历史
```
git reflog
```

### 搜索
```
git log --grep=hello
git log --author=wake
```

### 删除本次的add
```
git reset HEAD 文件名
```

### 查看当前项目下的分支
```
git branch
```

### 创建分支
```
git branch dev
```
### 切换分支
```
git checkout dev
```
### 删除分支
```
git branch -D dev
```
### 创建并切换分支
```
git checkout -b dev
```

### 合并分支
- 默认master是主干，用主干和并分支
```
git merge 分支名
```

> 合并分支后 被合并的分支删除即可

### 处理冲突
由于两个分支改变了相同的文件，但是内容不同这时候要手动处理，再次提交，就可以完成合并（模块化开发可以降低冲突）


### 创建有内容的文件
```
echo "内容"  > 文件名     向文件中写入内容，如果文件不存在会创建并写入
echo 'content'  >> 文件名 向文件中追加内容
```
### 关联仓库
```
 git remote add origin(名字)  远程地址http
```

### 推送到远程


-u upstream 设置后下次推送时可以直接使用git push 简写
推送到远程 git push origin(名字) master -u


### 忽略文件
- .gitiignore
要忽略的文件需要在.gitignore建立之后在add.
- git 不能提交空文件夹


 ###  在github 上发布静态网站
 
 >  必须在当前项目下建立一个gh-pages 的分支
 > 将需要发布的内容推送到gh-pages的分支上
 >  推送到远程仓库
 >  github会给你一个在线网址(在 gh-pages分支的settings中)

```
 git checkout -b gh-pages
 touch ind ex.html
 git add .
 git commit -m 'add index.html'
 git push origin gh-pages
在settings中可查找到网址+ 文件名即可 (默认会展示index.html)
```

###将文章发送给老师(通过github)
 - 老师   https://github.com/zhufengzhufeng/201701node_homework.git
 - 组长 
 组长 fork老师代码，你的代码和我的一样，我改变了代码不会自动同步你的项目
 - 组员
 组员fork组长的仓库

### 获取自己仓库的代码

```
git clone https://
```


###  git 提交作业

 **1**
- 组长fork 老师
- 组员fork组长

**2**
 - 组长克隆自己的代码
 - 组员也克隆自己代码

**3**
 - 组长建立自己组的文件夹，里面放入组员的信息
 - 组长提交到自己的仓库

**4 组员和组长建立联系**
```
//添加组长为远程仓库地址
git remote add leader 组长的地址
```

 **5 组员拉取组长最新代码**
```
git pull leader master
```
**6 将自己写的内容放到文件夹中**
**7 组员将内容提交到自己的仓库上**
**8 提交后发送pull request**
**9 组长合并**

