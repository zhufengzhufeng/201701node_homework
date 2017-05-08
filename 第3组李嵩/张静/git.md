
# node
安装git选择第三项，为了可以在dos命令下 使用git命令和linux命令
### DOS命令窗口中的一些常用的DOS命令
####- window+R键->运行命令处输入cmd
####- ipconfig  ipconfig -all  查看自己电脑的ip地址
####- ping www.baidu.com -t 查看自己的网络状况
####- ctrl+c  终止正在运行的DOS命令
####- exit  关掉DOS命令窗口
####- cls  清屏

####- cd ../返回当前文件夹中目录的上一级目录
####- cd ./当前目录
####- cd /返回当前磁盘的根目录
####- D: 直接进入到D盘
####- cd 文件夹名 进入到指定的文件夹中
####- dir 查看当前文件夹下的目录
####- 以上所有的操作基本上都是为了进入具体的某一个文件夹下操作，但是我们可以不必要这么纠结，我们可以直接找到对应的文件夹，在文件夹的空白处 shift+鼠标右键 =>在此处打开命令窗口
### 客户端和服务器端的交互模型
#### DNS解析
 DNS是一个网络服务器，我们的域名解析其实就是在DNS上记录一条信息记录
服务器的端口号（0-65535）
一般我们都把自己的项目发布到80或443这两个端口下
###引擎
 每一个浏览器都有自己的引擎，谷歌浏览器是v8引擎（webkit），火狐浏览器是Gecko引擎，IE浏览器是Trident引擎
###W3C
一个制定开发规范非盈利性机构组织  HTML/HTML5/CSS/CSS3...的规范都是由这个组织制定和管理的
###如何优化页面
- 减少资源请求数（减少http请求）
- css合并成一个 或者css不是很多的话采用内嵌式
- js合并成一个或者采用内嵌式 
- 图片合并（雪碧图技术/css Sprite）或者图片延迟加载
- ajax请求和资源文件的请求原理是一样的（ajax异步加载数据）
### api接口
- 后台定义一些数据，前台可以通过ajax来获取数据
- ajax（异步不刷新）
### crm用户（管理系统） 增删改查
- ERP企业管理系统 ，CMS内容发布系统
### url和http基础知识
### URI=URL+URN
### URL:统一资源定位符
- http://v.qq.com:80/index.html?name=zhufeng&age=7#bbs
- http: 传输协议  客户端给服务器端的内容和服务器端传递给客户端的内容都是通过HTTP传输协议进行传输的
- v:qq.com  域名
- 80  端口
- index.html  请求资源文件名    告诉服务器我需要请求的资源文件是谁
- ?name=zhufeng&age=7:URL问号传参    客户端传递给服务器端的内容（客户端可以把一些值传递给服务器端，服务器端依然可以把一些内容传递给客服端）
### 传输协议
- HTTP:超文本传输协议，除了传输文本以外，还可以传输其他的东西，无状态的协议  例如：XML等
- HTTPS：更加安全的HTTP
- FTP：文件传输协议（应用于把项目源文件传递到服务器上）（较大的工程）
###每一种协议会有一个默认找的端口地址
- HTTP默认会找服务器的80端口
- HTTPS默认会找服务器的443端口
- FTP默认会找服务器的21端口
### 路由
根据不同的路径，返回不同的内容
##初步了解node
### 服务器端的任务
- 创建一个服务，并且监听一个端口号（IIS、Apache、node）
- 在当前的服务中接收客户端请求的内容
- 然后把对应的数据或者内容返回给客户端
### 客户端的任务
- 发送请求（还可以给服务器传递点东西）
- 接收到服务器返回的内容并进行渲染解析
### JS
- js是一门运行在客户端的轻量级的脚本编程语言
- js目前不仅仅只能在浏览器中运行，还可以在node中运行
###什么是node
 node是一个环境，供js代码执行的环境，我们可以把他等价于浏览器，只不过我们一般都会把node这个环境安装到服务器端，这样的话我们就可以在服务器端使用js编写程序了，也就是说js不仅仅是客户端的语言也是服务器端的语言...
- 安装完成后，在dos命令行输入  node -v查看node版本
-  安装node会赠送一个包管理器   npm -v
### node和浏览器的区别：
- node采用的是谷歌的v8引擎来渲染js的（运行的速度快、稳定、我们编写的js代码不需要考虑兼容）
- 浏览器中的全局js对象是window，而node环境下的全局js对象是global
- 浏览器是安装在客户端的，为了保护客户端的安全，基本上不可能提供用js对客户电脑磁盘上的文件进行操作的功能；但是node环境中提供了对应的I/O操作（服务器上文件的操作），我们使用js可以对服务器磁盘下的文件进行增删改查
- node提供给js很多新的方法：http.createServer、fs.writeFileSync、fs.readFileSync...
- node是基于事件驱动的/异步编程（我们在node环境下编写的js程序一般都是异步bisa）
### node模块
#### 内置模块：node环境天生提供的

> http(creatServer..) 、fs（writeFilesync、readFileSync..）、url...
#### 自定义模块(文件模块)：我们自己定义的模块
- 如何声明一个模块（任何一个js文件都是一个模块）
- 导出一个模块：module.exports 或exports（单个文件导出用）
- 使用一个模块：require
```
module.exports={
  fn:fn
}
或者
module.exprots.fn=fn；
```

```
let fn=require('./a.js');
```
#### 第三方模块：别人写的，我们拿来用需下载  使用npm这个命令进行管理   http://www.npmjs.com 
- 下载第三方模块之前 初始化一个package.json用来记录下载的模块:npm  init
- 安装：npm install 第三方模块名称  --save（安装在node的全局环境中，  --save 开发上线都需要）
- --save-dev 开发时使用 ，上线不使用
- 卸载：npm uninstall 第三方模块名称   --save
- 把安装好的地方放模块导入到js中，我们就可以使用这个模块中的方法了
```
let mime=require('mime');
mime.lookup(pathname);
```
- 安装后会产生一个node_modules文件，不要更改文件名
### npm init
> npm init  -y  初始化

- 当前项目名字，不能有大写  空格  中文，不能叫你要安装的模块
- package.json 里面不能有任何的注释
### 断掉启动的服务：两次ctrl+c停掉此服务
###URL模块
 是node中自带的一个模块，解析路径的
```
let url=require('url');//处理路径的，可以将路径转换成对象
```
> 转换后的对象pathname属性就是真正的请求路径，query就是？号的值，query默认是字符串，需要转换成对象提供参数true可以转换成对象
```
let urlObj=url.parse(request.url,true);
let pathname=urlObj.pathname;//端口号到问号之间的内容 http://www.baidu.com"/s"?a=1
let query=urlObj.query；//查询字符串 a=1=>{a:1}
//综合起来写
let {pathname,query}=url.parse(request.url,true);
```
### HTTP
- http.createServer:创建一个服务
- server.linsten：为这个服务器监听一个端口
```
let server=htttp.createServer(function(request,response){
//当客户端向服务器端的当前服务发送一个请求，并且当前服务已经成功接收到了这个请求后执行这个回调函数
//request（请求）:存放的是所有客户端的请求信息，包含客户端通过问号传参的方式传递给服务器的数据内容
//request.url:存放的是客户端请求的文件资源的目录和名称以及传递给服务端的数据，例：客户端请求的地址：http://192.168.0.12/index.html?name=zhufeng&age=7我们服务端通过request.url获取到的是：/index.html?name=zhufeng&age=7
console.log(requret.url);
if(pathname=='/1.html'){
  let result=fs.readFileSync('1.html','charset=utf-8');
  //response(响应)：提供了向客户端返回内容和数据的方法
  //response.write：向客户端返回内容
  //response.end：告诉服务器响应结束了（一定要加）
  response.write();
  response.enc(result);
}
})
```
```
server.listen(80,function(){
//当服务创建成功，并且端口号也监听成功后执行
 console.log('server is create success!')
})
```
> get 获取资源 查询   浏览器只能发get请求    
> post 发送资源 保存
> delete 删除资源 删除
> put  修改资源 修改
> head 
> options 预发射，一般在发射post请求之前发送（跨域）
## get和post的区别
-两个都不安全，相对来说post安全一些
-get参数都是从url传递， post通过请求体传递

# Git
### pwd
> print working directory  打印当前工作命令
### 告诉git当前我是谁
> 用git第一次需要配置 以后都不需要，如果不配置则不能提交代码
```
git config  --global user.name  <github名字>
git config -- global user.email <github邮箱>
git config --list 查看配置列表
```
### 初始化文件夹（告诉git哪个文件夹归git所管理）（master主根）
```
git init
```
### cd
- change directory
### mkdir
- make directory
### 不能仓库套仓库
> 不能再初始化后的仓库下，在新建文件夹初始化仓库
### 查看文件夹中的内容
```
ls -a
```
### 删除文件夹
```
rm -rf .git
```
### 删除文件
```
rm -rf .index.txt
```
### 创建文件
```
touch index.txt
```
### 查看文件内容
```
cat index.txt
```
## vi 编辑内容
- 不能编辑文件夹，只能编辑文件
```
vi index.txt
i 插入模式
ESC :wq  保存并退出
q!  强制退出
```
### 查看git状态
- 工作区：红色
- 暂存区：绿色
```
git status
```
### 往暂存区上传（3种方式）
```
git add 文件名
git add .
git add -A
```
### 往版本库传文件（版本库的文件永远不会丢失）
```
git commit -m '消息'
```
### 查看版本
```
git log  看长的
git log --online  看短的
```
### 代码对比
- 工作区和暂存区
```
git diff
```
- 暂存区和版本库
```
git diff --cached
```
- 工作区和版本库
```
git diff 分支名
```

> 如果执行过一次增加到版本库 git commit -a -m 'write hello'

### 从暂存区将文件拿到工作区
```
git checkout 文件名
```
### 从版本库直接找一个版本覆盖掉工作区和暂存区(回滚操作)
```
git reset --hard 版本号
```
### 查看所有的版本号
```
git reflog
```
### 搜索日志
```
git log --grep=hello
git log --author=zhangjing
```
### 删除本次的add（加入暂存区后，返回上一次的添加）
```
git reset HEAD 文件名
```
### 查看当前项目下的分支
```
get branch
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
git branch -D dev(分支名)
```
### 创建dev并且切换到dev上
```
git checkout -b dev
```
### 合并分支
- 默认master是主干，用主干合并分支
- 合并分支后，被合并的分支删除即可
```
git merge 分支名
```
### 处理合并分支后的冲突
> 由于两个分支改变了相同的文件，但是内容不同这时候要手动处理，再次提交，就可以完成合并了（模块化开发可以降低冲突）

> q  退出命令行

### github注册之后需要配置邮箱

### 创建有内容的文件
```
echo 内容 > 文件名
echo 内容 >> 文件名(追加内容)
```
### 关联仓库
```
git remote add 名字 地址
```
### 推送到远
```
-u upstream 你设置后下次推送时可以使用简写
git push origin master -u
pit push
```
> git 不识别空文件夹，不能提交

### 忽略文件
- .gitignore
要忽略的文件需要在.gitignore建立之后在add

### 在github上发布静态网站
- 必须当前项目下建立一个gh-pages的分支
- 将我们需要发布的内容推送到gh-pages这个分支上
- 推送到远程仓库
- github会给你一个在线地址

```
git checkout -b gh-pages
touch index.html
git add.
git commit -m 'add index.html'
git push zhangjing gh-pages
在setting中可查找到网址+文件名即可（默认会展示index.html）
```


## 将文章发送给老师（通过github）
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



## 1.
- 组长fork老师
- 组员fork组长

## 2.
- 组长克隆自己代码
- 组员也克隆自己的代码

## 3.
- 组长建立自己组的文件夹，里面放入组员信息
- 组长提交到自己仓库

## 4.
- 组员和组长建立联系
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

## 5.
- 组长合并代码


## 组员要提交作业?
- 先获取组长的最新代码
- 放入自己的文件提交到自己的仓库上
- 发pull request请求

## 组长怎么提交给老师?
- 获取自己最新代码
- 获取老师最新代码
- 放入自己的文件，推送到自己的仓库上
- 发pull request请求

### 建立关系
```
git remote add  leader 别人地址
```
git push origin master  往github上推送东西


```
git remote -v   查看所有的管道
```




