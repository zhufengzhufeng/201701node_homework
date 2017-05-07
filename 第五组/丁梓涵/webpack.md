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
#### 下载hexo工具
```
npm install hexo-cli -g
```

> 下载后可以在命令行下生成一个全局命令叫hexo
#### 创建一个博客文件夹
```
hexo init 文件夹的名字
```
#### 进入这个文件夹
```
cd 文件夹的名字
```
#### 启动博客
```
hexo server -p 端口号
```

#### 发布到github上 一个账号只能发布一次
```
名字叫  zuyuan.github.io
```

#### 在conf.yml下进行配置
```
deploy:
  type: git
  repo: https://username:password@github.com/zuyuan/zuyuan.github.io.git
  brach: master
```
#### 下载发布插件
```
npm install hexo-deployer-git --save
```
#### 发布
```
hexo g 生成静态页
hexo d 发布
```
#### 查看博客
```
zuyuan.github.io
```

#### 找到theme
找到github地址,拉取到本地，更改_confg.yml 指定新的主题名字
```
hexo g
hexo d
```
#### 读和写(同步)
fs.readFileSync
fs.writeFileSync

#### 读和写(异步)
fs.readFile
fs.writeFile

#### 创建目录
fs.mkdirSync
fs.mkdir
## 发布自己的包
- 多个js文件组成的就叫包
- 通常包都存在一个入口文件(用来穿整个项目的)
- 发布这个文件夹(你发的包不能和已经存在的包名字相同)

```
npm init 
```
> 包中必须要有package.json

## 像npm官网发包
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

## 下载idoc
```
npm install fandoc -g
``` 
