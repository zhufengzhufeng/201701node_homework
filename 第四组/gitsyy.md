- vi编辑
```

```
- git branch查看 分支
- git branch dev创建分支
- git checkout dev 切换分支
- git branch -D dev 删除分支（先切换到主分支 git checkout master）
- git checkout -b dev 创建并切换分支
- 将文件提交到自己的身上
  - touch 1.js
  - git checkout dev
  - git add .
  - git commit -m "add"
- 默认master是主干，用主干合并分支（先切换到主分支 git checkout master）
  - git merge dev（现在2个分支都有1.js）
  - git branch -D dev(合并分支后，被合并的分支删除即可)
- 合并分支
   - git branch
   - git checkout -b dev（然后分别将文件提交到自己的身上）
   - 合并分支（git merge dev）
   - 由于2个分支改变了相同的文件，但是内容不同，这时候要手动处理，再次提交，就可以完成合并（模块化开发可以降低冲突）
- github配置后要配置邮箱
- 关联仓库 git remote add 名字


####忽略文件
- .idea
- node_modules
- bower_componets
- .DS_Store
####
- git不能提交空的文件夹（不识别）

####在github上发布静态网站
  - 必须当前项目下建立一个gh-pages的分支
  - 将我们需要发布的内容推送到gh-pages的分支上
  - 推送到远程仓库即可
  - github会给一个在线地址
      - git checkout -b gh-pages
      - 在文件夹（本地仓库）新建一个html文件
      - git add .（在文件夹下右键git bash）
      - git commit -m  "add 正方体.html"
      - git push origin gh-pages
###将文章发送给老师（通过github）
####第一步组长组员分工
   - 老师  
   - 组长：组长fork老师代码，你的代码和我的一样，我改变了代码不会自动同步你的项目
   - 组员 ：组员fork组长的代码
    
####第二步获取自己仓库的代码
   
   - 组长克隆自己的代码 （git clone+组长自己的地址）
   - 组员克隆自己的代码：`git clone https://github.com/hhhh4544/201701node_homework.git hhhh4544` （git clone+自己的地址）
  
####第三步 组长   
   - 组长建立新建文件夹 （在本地文件新建文件夹（放组员名称））
####第4步（组员和组长建立联系）  
   - 组员添加组长为远程仓库地址 `git remote add leader https://github.com/LuoYongGO/201701node_homework`（组长发过来的地址）
   - 将组长的代码拉到本地 `git pull leader master`
####提交自己的作业（到自己的仓库）   
   - 找到自己组建立自己的文件夹，放入自己的作业,提交到自己的仓库
      - git add .
      - git commit -m "xxx"(在根路径提交)
      - pull origin master （最终写好的代码）
####提交自己的作业（到组长的仓库）         
   - 将自己的代码发给组长
      - new pull request
      - create pull request
####组长合并组员作业     
   - 组长合并组员作业
      - merge pull request
####注意
   - 组员在提交之前 先获取组长的最新代码要拉取组长的  git pull leader master
   - 组长在提交之前 要拉取老师的  
      - git remote add teacher 地址（组长和老师建立联系）
      - git pull teacher master 
   - 组长提交 git pull origin master     
   - 组长提交到老师
      - new pull request
      - create pull request
####组员总结
1. 组员在提交之前 先获取组长的最新代码
2. 放入自己的文件提交到自己的仓库上
3. 发pull request请求
####组长总结
1. 获取自己最新代码
2. 获取老师最新代码
3. 
      