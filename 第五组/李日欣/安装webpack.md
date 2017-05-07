#### 安装webpack
```
npm install webpack -S
```
#### package.json中添加脚本
```
 "scripts": {
    "build": "webpack"
  }
```
#### 运行脚本
```
npm run build
```

#### 加载CSS
```
npm install style-loader css-loader -S
```

#### 加载图片
```
npm install url-loader
```

#### 把ES6编译成ES5
```
npm install babel-core babel-loader -S
npm install babel-preset-es2015 -S
```

#### 安装webpack-dev-server
```
npm install webpack-dev-server -S
```

#### 自动产出webpack文件
```
npm install html-webpack-plugin -S
```
## 同源策略
- 协议 主机名 端口号，有一个不一致 都会导致跨域问题
```
https://www.baidu.com
http://www.baidu.com
http://www.baidu.com:80
http://www.baidu.com:90
http://www.baidu1.com:80
http://www.baidu2.com:80
```
> 默认情况，自己的页面，访问自己服务器，不会出现跨域问题


## 两个网站要共享数据
jsonp 为跨域的最常见的手段（不能发数据，只支持get请求）
ajax会有限制问题，会出现不允许访问。
jsonp,cros,postMessage(iframe),websocket;

- jsonp:script不会导致跨域问题，我的网站引用你的网站的js,img,css,不用img和css的原因是默认会被转成图片和样式 ,img常用作记录访问页面的次数，统计请求这张图片的次数
- cros 让被访问的服务器 允许跨域即可 （需要服务端支持）

- iframe跨域 html5 提供的api

- websocket html5提供的api

> jsonp 是通过src跨域的 并且支持get请求
> 由于src没有访问限制，可以通过src 引用其他网站的数据 （此网站必须通过这样的接口）

## jsonp的原理
- 1.在当前js中声明一个全局函数
function fn(data){ 这里就是获取数据的地方}
- 2.动态创建script标签
通过script标签引用其他网址并且将这个全局函数名字传递给后台
```
<script src="http://l:3000?cb=fn">
```
- 3.后台返回函数执行
res.end('fn({name:1})');
#### 什么叫路由 : 不同的路径返回不同的内容, spa 不同的路径显示不同的组件
####   
    beforeCreate created beforeMount mounted
    beforeUpdate updated beforeDestroy destroyed
     全局注册，在所有实例中都可以使用
      组件需要行为，结构 数据
      组件的模板中只能有一个根元素