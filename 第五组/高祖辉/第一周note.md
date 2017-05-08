# 第一周
## 2017.4.18
### DOS命令

    ipconfig/ipconfig -all 获取本机ip详细地址
    ping www.xxx.com /ping www.xxx.com -t查看当前实时网速
    Ctrl+C停止正在执行的命令
    cls / clear 清屏
    cd+文件名 进入指定文件夹
    cd ../ 返回上一级
    cd ./当前目录
    cd /返回到根目录
    dir 查看当前文件夹下的文件,包含隐藏文件
    ls / ls -a/ ls -al/ ls -all显示所有文件，包括隐藏文件
    D:直接进入D盘
    tab帮助查找
    mkdir +目录名 创建目录
    touch +文件名 创建文件
    echo +（内容） > 文件名（包含后缀）创建文件
### 工作流程

       - 制定需求 pm 产品经理
       - ARP高保真原型图（线框图）
       - 设计，标尺寸 1366 960 640 750 414*3
       - 切图，转换成html
       - 写js 静态
       - 和后台确定接口（联调）Ajax
       - 提测
### node特点

>- 1、node只是一个运行环境，让js可以运行在服务器端。而浏览器端js的缺点：不能操作系统级的api，而且没有模块化。node可以操作系统，自带模块化。
    1)node增加了很多方法，http，fs，url
    2)commonjs规范（requirejs amd规范，依赖前置；seajs cmd规范，就近依赖）
>- 2、node是基于v8引擎，速度快。可以支持es6，不需要考虑兼容性问题。
>- 3、单线程，异步非阻塞型I/O，事件环;
>- 4、node全局对象不再是window，是global。此时，直接在文件中打印this是{}空对象，而不是global。    node中声明的变量和global上的变量不是一样的，没有带var的就是global上的，查找时先查找带var的
>- 5、node是基于事件驱动，发布订阅模式。on removeListener emit

### commonjs

>- 对模块化的规范，自带模块化
>- 如何声明一个模块（任何一个js文件都是一个模块）
>- 导出一个模块 module.exports/exports
>- 使用一个模块 require
>- `require可以引用一个文件，让其在这个文件下执行，是一个同步方法，将文件读写过来在执行。`

### 模块分类
    1、内置模块，http fs url
    2、自定义模块(文件模块)
    3、第三方模块
    插件，在node中如果需要使用别人的模块，需要使用npm这个命令进行管理。npmjs.com
    安装 npm install 第三方模块名称 -g（安装到NODE的全局环境中）
    卸载 npm unstall 第三方模块名称 -g
    
### Status Code
    2开头都是成功
    200：表示成功的返回了内容
    301：永久重定向
    302：临时重定向
    304：走缓存
    4开头都是客户端错误
    400：参数不正确
    403：没权限访问
    404：not found
    5开头都是服务器端错误
    500：内部错误
    503：没有做负载均衡
    
### 
    请求有三部分组成：请求行 请求首 请求体
    服务器端响应内容给浏览器：响应行 响应首 响应体
    
### Response Headers
    Connection:keep-alive 链接：保持链接
    Date:Tue, 18 Apr 2017 08:35:56 GMT 服务端响应浏览器的一个时间
    Transfer-Encoding:chunked 传输的方式 分段传输
    
### Request Headers
    Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8   接收的类型
    Accept-Encoding:gzip, deflate, sdch, br
    Accept-Language:zh-CN,zh;q=0.8  接收的语言
    Cache-Control:max-age=0  缓存
    Connection:keep-alive
    DNT:1
    Host:127.0.0.1:8080
    Upgrade-Insecure-Requests:1
    User-Agent:Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36  浏览器内核信息

## 2017-4-19

### url模块
    是浏览器上自带的一个模块，解析路径的。
    let url = require('url');
    将路径拆分成一个对象，true的参数会将查询字符串转换成一个对象
    let urlObj = url.parse(req.url,true);
    let pathname = urlObj.pathname 端口号到问好之间的内容 http://www.baidu.com"/s"?a=1
    let query = urlObj.query  查询字符串 a=1 =>{a:1}
    let {pathname,query} =  url.parse(req.url,true);
    
### 结构赋值
    es6语法
    {xxx,yyy}=object,当object中也具有这些属性名xxx，yyy就可以将object中的属性一个个拿出来
    当key和value相同时，就可以省略一个。
    
### 模板字符串
    在``中的都属于字符串，如果需要传入变量需要${xxx}。字符串中的'"需要转义字符\进行转义。
    
### 第三方模块
    1、npm init -y（一步yes到底）
    2、npm install mime(需要安装的模块) --save 表示开发和线上都需要
    npm uninstall mime --save-dev开发时使用，上线不使用
    3、安装后会产生一个node_modules文件，不要修改文件名
    
### npm init注意事项
    下载第三方模块之前，初始化一个package.json用来记录下载的模块
    1、当前项目名称，不能使用大写、空格，中文、
    2、package.json里面不能有任何修改
    
### 自动安装
    
    自己的代码发给别人时可能不会传递node_modules文件,由于package.json已经记录了可以通过 npm install 重新找回进行安装。
### Http动词
    1、get和POST
        get 获取资源，查询  post发送资源，保存；
        两者都不安全，相对而言post安全一些
        get参数都是从url传递，post通过请求体传递
    2、Delete 删除资源 ，删除
    3、普通 修改资源，修改
    4、HEAD
    5、options 预发射，一般在发送post之前发送跨域
    
### Ajax
    ajax分为四步：new open onreadstatechange send
    readyState的状态分为5种：
    unsent 0
    opened 1 打开
    HEADERS_RECEIVED 2 头接收完毕
    LOADING 正在加载中
    DONE 4
    
## 2017-4-20

### ajax
    ```
    var xhr = new XMLHttpRequest(); //UNSENT 0
    xhr.open('method','url?a=1&b=2',true);//true代表的是异步
    xhr.responseType = 'json';//设置服务端响应回来的类型
    xhr.onreadystatechange = function(){
        if(xhr.status == 200 && xhr.readyState==4){
            xhr.response;//自动就是对象，后台返回的结果（数据）
        }
    }
    xhr.send(JSON.stringify({name:1}))
    ```
### ajax传递数据
>- 解析路径

    ```
    'url?a=1&b=2'
    let {a,b} = url.parse(req.url,true)
    ```
>- 解析请求体

    ```
    xhr.send(JSON.stringify({name:1}))
    var str = '';
    req.on('data',function(data){
        str+=data;
    });
    req.on('end',function(){
        JSON.parse(str);
        res.end(JSON.stringify([]))
    })
    ```
## 本地搭建静态服务
>- 启动本地的html
```
    npm install http-server -g
```
## 2017-4-23
## 同源策略
   协议 主机名 端口号，有一个不一致 都会导致跨域问题
    ```
    https://www.baidu.com
    
    http://www.baidu.com
    
    http://www.baidu.com:80
    
    http://www.baidu.com:90
    
    http://www.baidu1.com:80
    
    http://www.baidu2.com:80
    
    ```
> 默认情况，自己的页面，访问自己服务器，不会出现跨域问题   
## 跨域请求
    jsonp 为跨域的最常见的手段（不能发数据，只支持get请求）
    ajax会有限制问题，会出现不允许访问。
    几种跨域的方式？jsonp,cros,postMessage(iframe),websocket;
    -> jsonp:script不会导致跨域问题，我的网站引用你的网站的js,img,css,不用img和css的原因是默认会被转成图片和样式 ,img常用作记录访问页面的次数，统计请求这张图片的次数
    -> cros 让被访问的服务器 允许跨域即可 （需要服务端支持）
    -> iframe跨域 html5 提供的api
    -> websocket html5提供的api
> jsonp 是通过src跨域的，并且支持只get请求
> 由于src没有访问限制，可以通过src引用其他网站的数据
## jsonp的原理
>- 1、在当前js中声明一个全局函数。function fn(data){这里就是处理 响应数据的地方}
>- 2、动态创建script标签通过script标签引用其他网址并且将这个全局函数名字传递给后台
    ```
    <script src="httr://:?">
    ```
>- 3、后台返回函数执行。response.end('fn({:})')
    

    
    
        
    
    
    
  
    
    

    
    