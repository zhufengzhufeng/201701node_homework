### git命令
1. git版本查询：git --version
2. git配置：git config --global user.name""/user.email""
3. git工作流程：
 - 创建文件夹
 - 配置git
 - git init  ，相当于建立本地仓库,初始化，但不能仓库套仓库，反初始化只需rm -rf .git，循环删除该文件即可，慎用
 - 登录[github](github.com)上创建远程仓库
 - git remote add pipeName +远程仓库地址，首次连接远程仓库
 - git remote -v 查看已建立远程仓库
 - git add .;git add -A,推送内容到远程仓库暂存区
 - git status: 查看状态
 - git commit -m"注释"，将内容推送到历史区(如果执行过一次版本库，可以连写git commit -a -m "注释"")
 - git log :查看日志|git reflog:查看此前操作过的版本号|git log --grep=版本，单独查看某个版本
 - git diff --cached:对比缓存区和版本库;git diff 对比工作区和缓存区|git diff branch对比工作区和版本库
 - git checkout 从暂存区将文件拿回
 - git reset --hard 版本号 ：将历史区直接回到之前的某个版本，覆盖工作区和暂存区
 - git reset HEAD . 加入暂存区后，返回上一次的添加
 - git push origin master,本地仓库内容推送到origin远程仓库master分支(可以使用 git push -u origin master,则下次可以使用简写 git push 即可)
 - touch .gitignore:忽略文件，写入一般需要忽略上传的文件.iea node_module .DS_store bower_computed 等忽略上传。
4. 拖拽他人项目
- fork,
- clone address
- 文件加下 使用git clone+address
5. 更新
  - 拖拽到本地之后，连接老师远程仓库 git remote add teacher +连接
  - git remote update teacher,更新库
  - git pull teacher master,更新teacher下的master分支的更新部分拉到本地
  - 将修改后的代码同步到个人远程库
  - 发送request 给teacher库
6. 移除远程通道
  - git remote rm 通道名称
7. 分支
  - git branch 查看分支
  - git branch dev 创建分支名为dev
  - git checkout dev 定位到dev分支
  - git checkout -b dev创建并定位到dev分支
  - git branch -D dev 删除dev分支
  - git merge dev 将dev分支合并到当前分支；当两个分支改变了相同的文件，但是内容不同，这时会出现分支合并冲突，请手动打开文件将不需要的删掉，并再次提交（模块化开发，降低冲突）。
8. cmd命令扩展
  - 创建文件夹：mkdir
  - 创建文档：touch
  - 查看文档：cat filename
  - 编辑文档：vi filename-->输入i,开启插入模式---》esc:(不保存!q|保存并推出wq)
  - print working directory 打印当前工作目录
9. 读写库文件
 - echo 'content' > filename 写入内容
 - echo 'content' >> filename,追加内容
10. 注意事项
 - git 不能提交空文件夹
11. 发布静态网站
 - 建立gh-pages
 git checkout - b gh-pages
 - 提交项目推送到远端
 