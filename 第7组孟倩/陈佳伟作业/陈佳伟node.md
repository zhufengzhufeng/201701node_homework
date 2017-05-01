###  node
####  node 是让js运行在服务端的环境
- commonjs   是个规范 ，这个规范定义了模块的定义（js文件），使用一个模块（require），导出模块
-  每一个js 文件都是一个模块 
-  使用模块用 require
-  提供一个专门操作文件的模块  fs
-  v8引擎，速度快， 不用考虑兼容性问题

#### 文件名不要使用中文，大写，特殊符
#### ajax+node
安装git选择第三项，为了可以在dos命令下 使用git命令和linux命令
#### 清屏clear
#### 查看所有文件ls -al
####改变目录change directory cd
#### 切换盘符 D:
#### 切换目录 cd 拖入文件
#### 在webStorm，点击view tool-window terminal
#### 创建目录 mkdir -p a/b
#### 创建文件 touch 文件名
#### 查看ip地址 ipconfig / ifconfig
#### webstrom注册码
http://idea.lanyus.com/
#### 全日制angular+react
#### 周末纯node

## 工作流程
- 制定需求 pm 产品经理
- ARP高保真原型图 （线框图）
- 设计，标尺寸 1366 960  640 750 414*3
- 切图，转换成html
- 写js 静态
- 和后台确定接口（联调） ajax
- 提测

## 后台php,java大数据,.net
## node（全栈工程师）
- node只是一个运行环境，让js可以运行在服务器端，浏览器端js的缺点，不能操作系统级的api，而且没有模块化，var obj = {} (function())(),node可以操作系统，自带模块化
    - node增加了很多方法，http fs
    - commonjs规范   (requirejs amd规范 依赖前置,seajs cmd规范 就近依赖)
- node是基于v8引擎，速度快
    - 可以支持es6,后台不需要考虑兼容性
- js单线程，异步I/O
    - 对文件操作时 同步和“异步”同时存在，能用异步绝不用同步
- node全局对象不再是window了，是global,直接在文件中打印this是{},并不是global
- node是一个基于事件驱动 （发布订阅模式）
    - on removeListener emit


## commonjs 
- 对模块化的规范，自带模块化
- 如何声明一个模块(任何一个js文件都是一个模块)
- 导出一个模块 module.exports  exports
- 使用一个模块 require

## 模块的分类
- 文件模块
- 核心模块，内置模块 http fs url...
- 第三方模块 别人写的 需要下载

## 第三方模块 （全局，本地的）
- 全局 只在命令行下使用(任何路径都可以)
```
npm install nodeppt -g
```

> nodeppt start 在当前目录下，启动ppt

## 断掉启动的服务
两次ctrl+c 停掉此服务
## url模块
是node中自带的一个模块，解析路径的
```
let url = require('url');
将路径拆分成一个对象，true的参数会将查询字符串转换成一个对象
let urlObj = url.parse(req.url,true);
let pathname = urlObj.pathname 端口号到问好之间的内容 http://www.baidu.com"/s"?a=1
let query = urlObj.query  查询字符串 a=1 =>{a:1}

let {pathname,query} =  url.parse(req.url,true);
```

## 解构赋值
把对象中的属性 一个个拿出来


## 安装第三方模块
```
npm init
```
## 第二部下载文件 jquery ejs mime
--save 开发上线都需要
```
npm install mime --save  安装
npm uninstall mime --save 卸载vv
```
--save-dev 开发时使用 ，上线不使用
 
> 安装后会产生一个node_modules文件，不要更改文件名。


## npm init 
- 当前项目名字，不能有大写 空格 中文，不能叫你要安装的模块
- package.json里面不能有任何的注释

## mime模块
这是一个别人写好的第三方模块 用来处理文件类型
```
npm init
npm install mime --save
require('mime').lookup('/index.css') => text/css
```

## 自动安装
自己的代码发给别人时可能不会传递node_modules文件,由于package.json已经记录了可以通过 npm install 重新找回进行安装。

## http动词
## GET 获取资源 查询
浏览器只能发get请求
1.GET和POST的区别  
2.两个都不安全，相对post安全一些
3.GET参数都是从url传递 POST通过请求体传递。
## POST 发送资源 保存
## DELETE 删除资源 删除
## PUT 修改资源  修改     
## HEAD
## OPTIONS 预发射，一般在发送post请求之前发送(跨域)

## 访问google商店下载插件
- 默认需要翻墙，greenvpn lattern 绿贝
- 更多-> 扩展程序 -> 获取更多扩展程序 jsonviewer 二维码 调试工具
#### 接口 api 
- 后台定义一些数据，前台可以通过ajax 来获取数据
-  ajax(异步不刷新页面)

####  crm 用户（管理系统） 增删改查
ERP 企业管理系统 CMS内容发布系统