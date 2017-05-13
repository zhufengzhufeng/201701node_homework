## express是后台框架
帮我们解决手动搭建服务，处理逻辑的复杂

```
npm init -y
npm install express --save  
```

## 使用postman模拟数据发送 (工具软件) 
https://www.getpostman.com/

> 测试接口是否可用

## 路由
根据请求的方法和请求的路径 返回不同的内容

```
app.方法('路径',callback);
app.all('*',callback)
```

> 匹配路由从上到下匹配，匹配成功后不继续向下执行

## express提供的属性
```
req.path
req.query
req.method
req.headers
```

## 路径参数params
- :id表示占位必须要有
```
app.get('/article/:id',callback)
```
- post请求查看路径
```
curl -X POST http://localhost:8080/home
```
- all代表所有匹配的方法,* 代表所有路径都可以匹配到，一般用来配置404页面，放到所有路由最下面，否则会被截断
```
app.all('*',function (req,res) {
    res.end('404');
});
```

## 中间件
中间件一般在路由上面写，错误中间件一般写在底部

- 扩展属性和方法，请求时中间件的res和req与路由中的是同一个
- 做权限处理，next可以决定是否向下执行
- 中间件可以写多个，和路由在同一个数组中
```
app.use('/',function(req,res,next){})
next表示是否向下执行
```

> 默认不写路径任何请求都能进行匹配

## send方法
- 不用设置类型
- 可以传递对象，数字会转化成状态文本

> 用send取代end
> 封装send方法
```
res.send = function (data) { 
        if(typeof data === 'string' || Buffer.isBuffer(data)){
            res.setHeader('Content-Type','text/plain;charset=utf-8');
            res.end(data);
        }else if(typeof data === 'object'){
            res.setHeader('Content-Type','application/json;charset=utf-8');
            res.end(JSON.stringify(data));
        }else{
            let result = require('_http_server').STATUS_CODES[data];
            //STATUS_CODES是所有网络状态码
            res.end(result);
        }
    };
```

## sendFile
- 像客户端返回单一页面
```
res.sendFile(path.resolve('./index.html'))
res.sendFile('./index.html',{root:__dirname});
```
## 静态服务中间件
> express提供了静态服务中间件

> 静态文件中间件可以配置多个

```
app.use(express.static(路径));
```

## 动态渲染ejs
- ejs(基于html，可以渲染动态数据) jade
- 如果安装了ejs ，如果使用render，express会自动调用ejs

```
app.set('views','新的路径');//views是系统默认名(不可改)，第二参数修改成的心路径名
app.set('view engine','html'); render时不需要提供html后缀
app.engine('html',require('ejs').__express);//html类型的用ejs来渲染
res.render('文件名',渲染的对象 = 自定义对象 + res.locals);
```

```//共有逻辑设置
app.use(function (req,res,next) {
    res.locals.title = 'zfpx'; //公有逻辑放到locals对象上
    next();
});
```

- Object.assign() 对象的拷贝

```
var obj1 = {name1:1};
var obj2 = {name2:2};
var obj3 = {name3:3};
var obj = Object.assign({obj1,obj2,obj3});
console.log(obj);//合并成-> obj={name1:1,name2:2,name3:3};
```

## ejs渲染数据
```
<%=%> 输出结果
<%for(var i = 0;i<arr.length;i++){%>
    <li><%=arr[i]%></li>
<%}%>
<%-%> 输出html
<%include ./header.html%>
```