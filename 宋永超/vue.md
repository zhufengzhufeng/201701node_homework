## 版本控制工具
git 和 svn 比较
git 比较快  分布式
svn 保存有一个。svn

pwd print working directory  打印当前工作目录

## 告诉当前
git config --global user.name github 名字
git config --global user.name 邮箱

查看配置列表  git config --list


mkdir  创建文件夹  mkdir git-test  创建了一个git-test文件夹
cd 改变目录

不能在初始化后的仓库 下的文件夹  在初始化仓库   只有一个仓库

ls 查看当前目录的文件列表  查不到隐藏文件
ls -a 查看隐藏文件
rm -rf 文件夹   rm 文件名  直接删除了

touch index.txt   创建文件
cat index.txt  产看文件内容
vi index.txt  是编辑文件内容  按i键出insert模式  可以打字  编辑完了 可以按esc  在输入:wq 是保存  如果不保存是 :q!是强制退出

git add 文件名 某个文件   git add -A  或者 git add .  提交所有文件
git commit -m "描述" 推送
git status 查看状态    add时候是工作区 红色的  暂存区是绿色  到版本库就不出来了  版本库里生成代码 不会丢失
esc :q  直接退出
git log 查看git 的版本  commit 后面是 还有日期 是版本  git log --online  简单版本
git diff 默认是工作区和暂存区比较  上面的是  暂存区  下面是工作区
git diff --cached 是暂存区和历史区比较  上面的是  历史区 下面是暂存区
git diff 分支名（仓库名） git diff master   上面的是历史区  下面的是 工作区
git checkout 文件名  git checkout .(代表全部)  就是把暂存区的代码  覆盖工作区了  原来工作取得代码  没用了  恢复原来代码
如果一个文件已经加到了历史库中  git commit -a -m '描述'  这样可以直接提交给历史区
git reset --hard 版本号  回滚到某个版本   之前的保留  之后的删除  直接回到了这个版本  这个版本就是  当时提交的时候  创建的版本
git reflog  查看所有操作的版本  包括删除的
搜索  git log --grep=hello提交的描述　　git log --author=用户名
已经提交给暂存区  又不要了 git reset HEAD 文件名  回重新回到 未提交的状态 暂存区
git branch 查看当前项目下的所有分支  * 代表当前所处分支
git branch dev-song  创建一个dev-song的分支
git checkout 'dev-song' 切换到dev-song的分支
git branch -D dev-song  把dev-song删除
git checkout -b dev-yong   创建dev-yong分支并且切换到dev-yong分支
刚创建的js  没有提交到分支  那么master其他分支也有  如果提交之后  这个文件只有自己有了  其他分支没有这个文件
用主干合并分支  先切换到master  git merge dev-song  把dev-song上面的代码  合并到master里面 合并完了以后master就有了dev-song里面的所有提交记录和版本号

echo "内容" > 文件名  会直接写到文件中  如果没有文件会创建文件在写入
echo 'content' >> 文件名  直接追加到文件中
关联仓库  git remote add 名字（origin） 远程地址http
推送到远程 git push -u 名字（origin） master  第一次加上-u  下一次就可以直接git push

git remote -v 查看最近关联的网址
git remote add o http.....
也可以删了  git remote rm o   删除o名字的关联远程
git不能识别空文件夹  不能提交

## 在github 上发布静态网站
 必须当前项目下建立一个gh-pages 的分支
 将我们的需要发布内容推送到gh-pages 这个分支上
 推动到远程仓库
 github会给你一个在线网址
 在gh-pages 分支的settings里面

 ##将文章发送给老师
 -老师

 -组长
   组长fork（叉子）老师的代码，你的代码和我的一样 我改变代码不会同步到你的项目中
 -组员
   组员fork组长的仓库