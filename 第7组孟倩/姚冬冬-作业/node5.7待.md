## node

### node是异步操作，基于回调函数

### js中哪些是异步的
- 定时器
- 事件触发
- ajax
- 回调函数

### 阻塞非阻塞
针对的内核，厨师，如果厨师不释放掉服务员，主线程不可能异步

- 非阻塞是异步的前置条件

> 主线是单线程的，内核是多线程的

### 单线程&多线程
- 一个个发短信
- 群发短信多线程

> 进程包括线程，在node中一个进程只能包括一个线程，node可以开多个线程，开多个进程（子进程）

### 事件循环
- 事件驱动

### global全局对象，window是浏览器的全局对象


## 模块
### 安装模块 
- npm root -g 可以查看安装到哪里去了
- 全局安装 -g 在命令行下使用
- nrm 切换源的工具
默认下载从官方下载npm,想从国内下载
```
npm install -g nrm 
```
- 查看所有可用的源
```
nrm ls
```
- 添加源
```
nrm add zf http://172.18.0.188
nrm del 源的名字
```
- 使用源
```
nrm use zf
```
- 测试源的速度
```
nrm test
```
### **本地安装(如果切换到淘宝后，以后都是通过淘宝进行安装)**
- 本地安装主要在项目中使用
- 如果没有初始化package.json可能会安装上一node_modules目录
```
npm init -y
npm install jquery --save 
npm uninstall jquery --save 卸载
```
#### 项目依赖
- 上线需要开发时也需要 mime
```
--save可以简写 -S
```
#### 开发依赖
- 上线不需要，开发时需要 webpack gulp
```
--save-dev 可以简写 -D
```
#### 安装依赖
- 当我们文件上传到github上，会node_module文件忽略掉，别人下载代码后需要执行npm install 将所有依赖进行安装
```
npm install
```

#### 安装指定版本
```
npm info jquery 查看版本
npm install jquery@2.2.2 
```

> 本地安装会默认安到node_modules中，package.json可以记住安装过的文件。

## yarn
- 也是安装模块的方式,和npm一样。
```
npm install yarn -g
```
- 初始化package.json
```
yarn init -y
```
- 安装模块
如果是项目依赖则不用标注，如果是开发依赖需要标注(-dev)
```
yarn add jquery
yarn add gulp -dev
yarn remove gulp -dev
```
- 安装依赖
```
yarn install
```

## 核心模块
内置的，node自带的模块


### 模块分类
- 文件模块
- 内置模块
- 第三方模块


### module
> 五个形参在文件中可以直接使用
>- exports 导出
>- module  模块
>- require 需要
>- __dirname  代表当前文件所在的目录 绝对路径
>- __filename 代表当前文件的目录    绝对路径
console.log(__dirname); // G:\前端培训\课件\node\node\2.node
console.log(__filename);//G:\前端培训\课件\node\node\2.node\2.module.js


**commonjs**
>- 1.如何定义模块 创建一个js文件
>- 2.如何使用模块 require
>- 3.如何导出模块 exports / module.exports
>-  module.exports适合导出对象类型; exports适合单个导出
### promise 
> 出现最早是用来解决回调嵌套的问题的
> 异步读取函数中的形参 err 错误对象 data 返回的文本内容
 
 **异步读取嵌套文件**
 
    fs.readFile('./1.txt', 'utf8', function (err,data) {//2.txt
    fs.readFile(data, 'utf8', function (err,data) {//3.txt
        fs.readFile(data,'utf8', function (err,data) {//3
            console.log(data);
        });
    })
      });
> promise内部会封装一个异步的任务，当new 一个Promise实例的时候，任务就开始执行了
>  创建一个promise对象  状态为初始态

**封装的Promise方法**
 
    //resolve 解决  reject 拒绝
    class Promise{
     constructor(fn){
        let resolve = (data)=>{
          this.onSuccess(data);
      };
        let reject = (err)=>{
          this.onFail(err);
      };
        fn(resolve,reject);
         }
              //onSuccess成功的回调 onFail失败的回调
    then(onSuccess,onFail){
    this.onSuccess = onSuccess;
    this.onFail = onFail;
       }
       }

      module.exports = Promise;


**Promise类创建实例的应用:**

    let fs = require('fs');
    let Promise = require('./Promise.js');
    let promise = new Promise(function(resolve,reject){
     fs.readFile('1.txt','utf8',function(err,data){
         if(err){//err有值表示此任务失败了
         //如果任务失败了，会调用reject方法
             reject(err);
         }else{
         //如果任务成功了，会调用resolve方法
             resolve(data);
         //1.会把promise状态改为成功态
         }
     })
    });
     //1 成功的回调函数 2 失败的回调函数
     promise.then(function(data){
    console.log(data);
    },function(err){
    console.log(err);
    });

> extends表示继承
> - class Student extends Person()

## publish 发布自己的包
- 多个js文件组成的就叫包
- 通常包都存在一个入口文件(用来穿整个项目的)
- 发布这个文件夹(你发的包不能和已经存在的包名字相同)

```
npm init 
```
> 包中必须要有package.json

### 向npm官网发包
- 切换到官方npm
```
nrm use npm
```
- 如果有账号表示登录 没账号表示注册
```
npm addUser
```
- 发布
```
npm publish
```

### 下载idoc
```
npm install fandoc -g
``` 

## event 事件
> 发布订阅模式
- 一种一对多的关系，订阅事件和发布事件
- {'水开了':["泡面","洗澡"]}

> 绑定事件on

> 发射事件emit

