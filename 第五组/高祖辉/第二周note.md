# vue
## 2017-4-26
## 数组方法（find、map、filter、reduce、循环）
## find 
    forEach没有返回值，不能中断循环
    find方法是es6中的方法（不兼容）
    1、在数组中查找，如果返回true表示找到了，找到后将当前item返回，如果没有找到则返回undefined    
    2、查找到就停止循环
```
    let ary=[{name:1},{name:2},{name:3}];
    let obj=ary.find(function(item){
        return item.name==2;
    })
```
## map
    映射：将一个数组变成另一个模样，用于修改
    返回值是新数组，不会改变原数组，4
```
    let ary=[{name:1},{name:2},{name:3}];
    let temp={age:2};
    let newAry=arr.map(function(item){
        if(item.name==2) return temp;
        return item;//不写此项会导致返回undefined
    })
    
```
## filter
    在函数中返回true表示这一项留下，返回false表示这一项删除
```
    let ary=[{name:1},{name:2},{name:3}];
    let newAry=ary.filter(function(item){
        return item!=2;//删除某一项没有塌陷问题
    })
```
> 声明（不关心如何实现，按照方法来用就行）

> 命名式（自己写的方法）

## for in/forEach/for of的区别
    for in 
    1、遍历数组时，key是字符串类型
    2、会遍历私有和公有属性（不想遍历的私有属性也会被遍历出来）
    
    for of
    1、可以跳出循环
    2、只会遍历数组中的内容for(let value of ary){//value代表数组中的每一项}
    3、不能遍历对象

## reduce
    返回的结果多次叠加的操作，你还可以手动指定默认的第一项是多少
    let ary=[1,2,3,4,5,6];
    let n=0;
    ary.reduce(function(prev,next){
        return prev+next
    },50)//50是第一次默认的返回值
    二维数组  扁平化
    let arr=[['1'],['2'],['3']];
    let newArr=arr.reduce(function(prev,next){
        return prev.concat(next);
       prev['1']，next['2']
       prev['1','2']，next['3']
    })
## 模式
>- 1、MVC
    M model 数据
    V view 视图
    C controller 控制器
    当用户改变页面时，会触发控制器，控制器会调用数据，将数据展示到对应的视图上
>- 2、MVVM
    M model (数据)
    V view  （页面DOM）
    VM viewModel 视图模型(监控者)
    先将数据绑定在视图模型上，会监听视图的改变，视图改变后会触发数据的变化，这种实现是通过VM。
>- MVVM框架，属于MVVM的JS框架除了Vue.js,还有React.js，Angular.js

## 亚索和不压缩的区别
    压缩后再写代码时，没有任何警告。一般开发选择未压缩的
   
## Vue的优点
    核心只关注视图层（view）
    易学，轻量，灵活
    适用于移动端项目
    渐进式框架
    
## Vue的核心
    通过尽可能简单的API实现响应的数据绑定和组合的视图组件
    1、数据绑定：数据改变驱动视图的自动更新，不用操心DOM
    2、视图组件：把整个网页拆分成一个个区块，每个区块可以看做一个组件，网页由多个组件拼接或者嵌套组成
>- Vue的核心实现使用了ES5的Object.defineProperty特性  
## vue
    npm info vue
     
    npm init -y 
    npm install vue --save
## 指令
    指令是一种特殊自定义行间属性，在Vue中，指令以v-开头
    
## 组件
    组件化就是把页面种特定的区块独立抽出来，并封装成一个方便复用的组件
## vue
    v-model(`双向绑定数据`，只能在表单元素上使用，将数据绑定在表单元素上，如果表单内容更改，会导致数据变化)
    v-html(可以将字符串的HTML转化成html)
    v-once (数据绑定一次，随后数据变化，不更新视图)
    v-text（和{{}}用法一致，用来将数据显示在视图上，防止单个元素闪烁）
    v-for（循环数组，对象，字符串 v-for="value of/in items"）
    v-on(可以绑定事件 v-on:事件名="函数名"，可以把v-on简写成@符号)
    v-show/v-if(控制元素的显示和隐藏，v-show控制的是样式，v-if控制的是dom元素的增加和删除)