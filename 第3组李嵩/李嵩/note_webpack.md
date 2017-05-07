#### webpack
强大的加载器和打包器
打包工具发展历程：grunt-》gulp-》webpack-》rollup
webpack是以commonJs形式来写，但对AMD/CMD的支持很全面，方便项目进行代码迁移
能被模块化的包括js和其他文件
#### webpack使用
1. 安装
```
npm install webpack --save-dev
```
2. 新建webpack.config.js
3. 再上述文件中建立入口和出口
```javascript
/**
 * Created by 40681 on 2017/5/3.
 */
let path = require('path');
module.exports = {
    //入口，打包的时候先找到这个文件，让后把这个文件及依赖的其他模块都打包到一个文件里
    entry:'./src/index.js',
    //指定如何输出
    output:{
        path:path.resolve('./build'),//输出目录,解析目录，将相对变绝对
        filename:'bundle.js'//输出的文件名
    }
};
```
4. package.json
添加脚本，'build':'webpack'
5. 运行脚本
```
npm run build
```
6. 加载图片
```
npm install file-loader
npm install url-loader
```
7. babel 
```
npm install babel-loader
npm install babel-core
然后配置loader
新建.babelrc:
加入：{"preset":["es2015"]
```
8. 开发服务,预览项目，并且可以自动打包
```
npm install webpack-dev-server 
```
9. 安装plugin,自动生成webpack
```
npm install html-webpack-plugin -S
```
