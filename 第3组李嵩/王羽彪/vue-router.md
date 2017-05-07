---
title: '''vue-router'''
date: 2017-05-04 09:46:51
tags:
---
## 安装
```
    npm install vue vue-router bootstrap animate.css --save
```
## 不切换页面,展示不同的内容
- html部分
```html
<!--路由的链接-->
<div id="app">
       <router-link to="/home">home</router-link>
       <router-link to="/list">list</router-link>
       <!--当路由匹配到后,会将组件插入到router-view中-->
       <router-view>

       </router-view>html
</div>
```
- js部分
```js
      //什么叫路由：不同的路径返回不同的内容,span 不同的路径显示不同的组件
        var home = {
            template: '<div>首页</div>'
        };
        var list = {
            template: '<div>列表页</div>'
        };
        //默认是hash #home
        const routes = [
            {path: '/home', component: home},
            {path: '/list', component: list}
        ]; //路由映射表
```
- 默认页面首先router-view是空的,因为没有进行过匹配
    1. 配置一个默认页面
    2. 直接跳转到某个hash
- 页面跳转
    - router.push('/aaa') 跳转页面,会产生历史管理
    - router.replace('/aaa') 会跳转页面,不产生历史管理

## 常用方法
 - router.beforeEach(to,from,next) 当路由切换的时候,会触发这个函数,范围最大,任何路由切换都会触发此函数 三个参数
    1. to 去哪个路由
    2. from 从哪个路由来
    3. next 表示是否向下执行,是一个函数如果调用next()表示继续,否则卡在这个不动
 - beforeEnter(to,form,next)
 - beforeRouteEnter(to,form,next)