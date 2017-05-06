github

1print working directory  打印当前工作目录
2告诉git 到当前我是谁
3 git config --global user.name  github 名字
4 git config --global user.email github 邮箱
5git config --list 查看配置列表  如果不配置不能提交代码
6ls -a 查看文件中的内容
7rm rf .get 删除文件夹
8cat 查看文件内容
9vi index.txt 编辑文件 i输入模式 esc切换 :wq保存退出 :q!强制退出
10 rm index.txt 删除内容 
11 git status 查看状态 红色表示工作区 绿色表示占存区
12 git log 查看提交信息 git log --oneline看起来简洁一些
13 git diff 比较  直接修改看的是 工作区 跟占存区
14 git diff --cached 强制用占存区和 版本区比较 什么不显示就是相同
15 git diff  master 工作区和版本区比较 
16 gitcheckout index.txt 从占存区 撤销到 工作区 关闭从新打开才能看见变化
17 git commit -a -m "提示信息"  已经添加到过历史区的可以这么使用 直接修改到 历史区
18 git reset --hard 版本号 将历史区直接找一版本覆盖掉工作区和占存区[回滚某个版本]
19 git reset --hard 版本号     切换版本git log --oneline 撤销之前要记住所有版本号,否则想回退 就找不到版本号了()
可以找到了 哈哈哈  git reflog 查看所有版本号
20 history>1.txt 记录操作的命令
21 git log --grep=提交过给的消息 搜索某一个版本
git log --auth=wake
git log --author=wake
git log --author=用户名
23 git reset HEAD index.txt 加入占存区后,返回上一次添加的内容
24 echo "内容" > 文件名 创建有内容的文件
24 echo "内容"  >> 文件名 追加文件内容
初始化文件夹 (告诉git那个文件夹归git管理)
mkdir git-test 创建文件夹 
cd git-test 进入这个文件夹
git init 初始化文件夹  (看隐藏的.git)
rm -rf .git  循环删除

创建的内容都在工作区中 

放到占存区 
git add.
git add -A
git add 文件名

放到历史区 :会生成版本永不会丢失
git commit -m "first"

以上区域都是本地区域 都在.git文件夹中


查看当前项目下的所有分支

git branch 查看分支
git branch 分支名 创建分支
git checkout 切换分支
git branch -D 删除分支 必须不在自己分支上才能删除
git checkout -b 分支名 创建并切换分支 


默认master是主干  用主干合并分支 而不是用分支合并主干
git merge 分支名 合并分支

分支或主干陈要有内容的提交

处理冲突
由于两个分支改变了相同的文件,但是内容不同这是要手动处理,就可以完成合并


管理仓库 git remote add 关联名字 地址
推送远程 -u upstream 你设置后下次可以简写
git push origin 

git remote -v 查看 

在github 上发布静态网站
必须在当前项目下建立一个 gh-papes 的分支
将我们需要发布的内容推送到 gh-pape这个分支
推送 到远程仓库即可
github 会给你一个在线地址



创建一个分支 git checkout -b 分支
touch index.html 
git add 
git commit -m "描述"
git push origin 分支
在settings 中找到网址 + 文件名 即可 (默认打开跟目录)


将文章发送给老师 通过github

组长
	组长fork(叉子) 老师代码,你的代码和我的一样,我改变的代码不会同步你的项目
组员
	组员fork组长


获取自己仓库的代码
git clone 地址          起别名可以name

克隆下来的代码就不需要走关联那步 直接推送 git push origin master




添加组长为远程仓库地址 git remote add chengxiao https://github.com/GayeChen/201701node_homework  
获取组长的文件内容 git pull chengxiao master

找到自己组 创建文集夹  创建文件
将自己的文件 推送到 自己的远程仓库	



-组长fark 老师 组员fark 组长
1)  fark 组长  克隆自己地址
2) git clone https://github.com/wj15510151110/201701node_homework.git
3) 组长建立自己组的文件夹 放入自己组的组员信息 提交到自己的仓库 1git add . 2git commit -m "信息"  3git push origin master
4) git remote add chengxiao https://github.com/GayeChen/201701node_homework  
5)git pull chengxiao master
6) 将自己的内容放到文件夹中
7)将自己的内容提交到仓库中
8)提交后 pull request 按钮
9 组长 合并代码

上传时间2017年4月29