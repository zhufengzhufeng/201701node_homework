## git 
### 本地git操作
>- pwd  print working directory 打印当前工作目录
> 告诉git 第一次需要配置 以后都不需要，如果不配置则不能提交代码

```
git config --global user.name <github用户名字>
git config --global user.email <github邮箱>
git config --list 查看配置列表
``` 
>- 初始化文件夹（告诉git 哪个文件夹归 git所管理）
```
git init
```
>- cd 改变路径
   - change directory

>- mkdir 创建文件夹
>- 删除文件夹    rm  -rf <文件夹名>
>- 不能那个仓库套仓库
    - 不能在初始化后的仓库下，在新建文件夹初始化仓库
 
>- 查看文件列表
```
ls -a 
```
>- 创建一个文件  touch 文件名
>- 删除文件         rm   文件名
>- 查看文件内容  cat  文件名


### 编辑文件内容
 -  不能编辑文件夹
```
vi 文件名
i  插入模式
ESC  :wq 保存并退出
ESC  q!  强制退出
```

### 提交
-  提交的内容，提交到暂存区
```
git add .
git add -A
git add 文件名
```

- git status  查看git状态
```
工作区 - 红色   暂存区 -绿色
```

### 添加到历史区
```
  git commit -m "msg"
 如果之前执行过提交，可以
    git commit -a -m "msg"
```
-  查看提交日志/ 版本号
```
git log 
git log  --oneline
```

### 比较
 >- 比较工作区和暂存区
   git diff
 >- 比较暂存区和历史区
   git diff  --cached
 >- 比较工作区和历史区
   git diff   master(分支名)

- 从暂存区将文件拿回来
   git  checkout 文件名
- 回滚：将历史区直接找一个版本覆盖掉暂存区和历史区
  git  reset  --hard (版本号)

- 查看版本历史
 git reflog
-  搜索
  git log --grep=hello
  git log --author= wake

- 删除本次的add
  git reset HEAD 文件名

### 分支
>-  查看当前项目下的分支
   - git branch 

>- 创建分支
   - git branch  dev
  
>- 切换分支
  - git checkout dev
 
>- 删除分支（在主分支上）
   - git branch -D dev
  
>- 创建并切换分支
  - git checkout -b dev

>- 合并分支
   - 默认master 是主干
   - 主干合并分支
   - git merge 分支名

>- 合并分之后 ，被合并的分支删除即可
>- **处理冲突：**
   -  由于两个分支改变了相同的文件，但是内容不同这时候要手动处理，再次提交，就可以完成合并（模块化开发可以降低冲突）


### 远程 git

> - github 注册之后需要配置邮箱
> - 创建有内容的文件
```
echo 内容 > 文件名
echo 内容 >>文件名(追加内容)
```

>- 关联仓库
  -   git remote add 名字  地址

>- 推送到远程
  -u  usptream 设置后下次推送时可以使用简写
  git push origin master -u
  git push 

>- 忽略文件
  - .gitignore  要忽略的文件需要在.gitignore 简历之后再 add


**git 不能提交空文件夹**


#### 在github上发布静态网站
 >- 必须当前项目下简历一个 gh-pages 的分支
 >- 将我们需要发布的内容推送到 gh-pages这个分支上
 >- 推送到 远程仓库上即可
 >- github 会给一个在线地址
 
 ```
  git  checkout -b gh-pages 
  touch index.html
  git add .
  git commit -m "add index.html"
  git push origin gh-pages
  在settings 中可查找到网址+文件名即可
 ```


### 如何将文章发送给老师（通过github）
- 老师 https://github.com/zhufengzhufeng/201701node_homework.git
- 组长   
 组长fork（叉子）老师代码，你的代码和我的一样，我改变了代码不会自动同步你的项目
 - 组员
组员fork组长的仓库

## 获取自己仓库的代码
```
git clone https://github.com/wakeupmypig/201701node_homework.git leader
```

## 组长克隆自己的代码
- 1.组长建立文件夹
- 2.推到自己的仓库上
## 组员克隆自己的代码
- 3.添加组长为远程仓库地址
```
git remote add leader 地址
```
- 4.拉取组长最新代码
```
git pull leader master
```
- 5.找到自己组建立自己的文件夹，放入自己的作业
- 6.提交到自己仓库上
- 7.发送pull request
- 8.组长合并



##### 1.
- 组长fork老师
- 组员fork组长

##### 2.
- 组长克隆自己代码
- 组员也克隆自己的代码

##### 3.
- 组长建立自己组的文件夹，里面放入组员信息
- 组长提交到自己仓库

##### 4.组员和组长建立联系
```
git remote add leader 组长的地址
```
- 组员拉取组长最新代码
```
git pull leader master
```
- 将自己写的内容放到文件夹中
- 组员将内容提交到自己的仓库上
- 提交后发送pull request

##### 5.  组长合并代码


## 组员要提交作业?
- 先获取组长的最新代码
- 放入自己的文件提交到自己的仓库上
- 发pull request请求

## 组长怎么提交给老师?
- 获取自己最新代码
- 获取老师最新代码
- 放入自己的文件，推送到自己的仓库上
- 发pull request请求