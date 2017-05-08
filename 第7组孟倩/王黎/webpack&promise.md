## ES6 webpack 

### 创建一个实例来继承父类的私有属性
**ES5**
```
//静态方法
function Person(name){
 this.name = name;
}
Person.prototype.getName = function(){
    console.log(this.name);
}
//静态方法
Person.add = function(a,b){return a+b}
function Student(name,age){
 Person.call(this,name);
 this.age = age; //继承了私有属性
}
//让子类的原型prototype等于父类的一个实例，通过 Object.create(Person.prototype)只继承私有属性
Student.prototype = Object.create(Person.prototype);
//create原理
function create(prototype){
    function Fn(){
        Fn.prototype = prototype;
        return new Fn();
    }
}
Student.prototype.constructor = Student;
Student.prototype.getAge = function(){
    console.log(this.age);
}
let s = new Student('zfpx2',8);
s.getName();
s.getAge();


//ES6方法
class Person{
    //构造函数 当通过创建一个实例的时候就会使用此构造函数
    constructor(name){
        this.name = name;
    }
    //定义所有实例公有的方法
    getName(){
        console.log(this.name);
    }
    //表示静态方法，是属于类的方法，不需要创建实例来调用
    static add(a,b){
        return a+b;
    }
    let p = new Person('zfpx');
    p.getName();
    console.log(Person.add(1,2));
    //extends 表示继承
    class Student extends Person{
        constructor(name,age){
            //super表示父类的构造函数
            super(name); //在此方法里，this指向的是子类的实例
            this.age = age; //再初始化自己的私有属性
        }
        getAge(){
            console.log(this.age);
        }
   }
}
```

### module

**导出对象**

```
 var name = 'zfpx';
 var age = 8;
//export是一个关键字，表示把此对象导出
export {name,age};  //ES6写法
// 也可以在需要导出的变量前加 export
export var name = 'zfpx';
export var age = 8;

//commenjs 方法，一般在node中使用，浏览器支持不太好
module.exports = {name,age};

//default 默认导出
export default class Person{
    constructor(name){
        this.name = name;
    }
}
```

 **接收对象，解构赋值 **

```
import {name,age} from './component.js';
console.log(name, age);
//如何在不知道要导入的模块内部有哪些变量的情况下进行接收
import * as obj from './component.js';
console.log(obj.age);

import Pes from './component.js';
let p = new Pes('zzz');
console.log(p); //Person {name:'zzzz'}
```

### promise

**promise **出现最早是用来解决回调嵌套的问题的，可采用链式调用方法
- 内部会封装一个异步的任务，当new 一个Promise实例 的时候，任务就开始执行了
-  创建一个promise对象，状态为初始状态
-  resolve 解决     reject 拒绝

```
//写一个Promise类
class Promise{
    constructor(fn){
        let resolve = (data)=>{
            this.onSuccess(data);
        }
        let reject = (err)=>{
            this.onFail(err);
        }
        fn(resolve,reject);
    }
    then(onSuccess,onFail){
        this.onSuccess = onSuccess;
        this.onFail = onFail;
    }
}

module.exports = Promise;
```

```
//1.txt->2.txt->3.txt->3
let fs = require('fs');
let Promise = require('./Promise.js');
let promise = new Promise(function(resolve,reject){
    fs.readFile('1.txt','utf8',function(){
        if(err){//err有值表示此任务失败了
            //如果任务失败了，会调用reject方法
            reject(err);
        }else{
            //如果任务成功了，会调用resolve方法
            resolve(data);
            //会把promise状态改为成功态
        }
    })
})
//promise中的then方法：1成功的回调函数；2失败的回调函数
promise.then(function(data){
    console.log(data);
},function(err){
    console.log(err);
})
```

**$.ajax获取返回值有三种方法：1.success;2.then;3.done**

#### ajax 结合promise.then方法获取数据
- 1.要返回一个promise
- 2.在promise的参数中需要开启一个ajax调用,如果调用成功用resolve,如果调用失败，调用reject
- 3.map方法 ：
```
 [4,1,2].map(num=>num*2);  //[8,2,4]
```

  
```
 function ajax({url,type,dataType}){
    return new Promise(function(resolve,reject){
        let xhr = new XMLHttpRequest();
        xhr.open(type,url,true);
        xhr.responseType = dataType;
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4 && xhr.status == 200){
                resolve(xhr.response);
            }else{
                reject(xhr.response);
            }
        }
        xhr.send();
    })
}
ajax({
    url:'users.json',
    type:'GET',
    dataType:'json',
}).then(function(result){
    //{"id":1,"name":"zfpx1"} => <li>1:zfpx1</li>; map方法后获取的是li数组
    let html = result.map(user=> `<li>${user.id}:${user.name}</li>`).join('');
    //['<li>1:zfpx1</li><li>2:zfpx2</li><li>3:zfpx3</li>']
    document.querySelector("#users").innerHTML = html;
})
```

### webpack

```
//安装webpack
npm install webpack -S 
//package.json中添加脚本
"scripts":{
    "build":"webpack",
    "dev":"webpack-dev-server"
}
// 运行脚本
npm run build
//加载css
npm install style-loader css-loader -S
//加载图片
npm install url-loader
// 把ES6编译成ES5
npm install babel-core babel-loader -S
npm install babel-preset-es2015 -S
//安装webpack-dev-server
npm install webpack-dev-server -S
//自动产出webpack文件
npm install html-webpack-plugin -S
```

