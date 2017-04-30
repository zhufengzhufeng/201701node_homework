# vue
### find方法  查找
> 在数组中查找，如果返回true，表示找到，找到后会将当前item返回，如果没有找到则返回undefined
> 只查找一次，查找到后停止循环

```
let arr=[{name:1},{name:2},{name:3},{name:2}];
let obj=arr.find(function(item){
  return item.name==2;
});
console.log(obj);
```

### map 修改
> map:映射  将一个数组变成另一个摸样
> 返回值是一个新数组，不会改变原数组，会将返回的值替换当前项
```
let arr=[{name:1},{name:2},{name:3},{name:2}];
let temp={age:2};
let newArr=arr.map(function(item){
 if(item.name==2) return temp;
 return item;
}) ;
console.log(newArr);
```
### filter 过滤  删除
> 返回一个新数组 返回true这一项便留下，返回false便是将这一项删除
```
let arr=[{name:1},{name:2},{name:3},{name:2}];
//声明式（不关心怎么实现，按照方法用则可以）
let newArr=arr.filter(function(item){
return item.name!=2;//如果想删除这一项，都用!=;
});
console.log(newArr);
//命令式
for(let i=0;i<arr.length;i++){
  let cur=arr[i];
  if(cur.name==2){
  i--;
  }
}
console.log(arr);
```
### for in ,forEach  ,for  of的区别
> for in 缺点：1.key是字符串类型的，2. for  in 会遍历私有和公有属性（不想遍历的私有属性也会被遍历出来）
> forEach没有返回值，不会终止循环
> for  of  优点：1.可以跳出循环 2.只会遍历数组中的内容  3.缺点：不能遍历对象
```
let arr=[1,2,3,4];
arr.name='jw';
for(let value of arr){
console.log(value);//value  代表数组的每一项的值
}
```
### reduce  es5语法  收敛
> 返回的结果是多次叠加的操作，自己制定首次默认的第一项是多少
```
let arr=[1,2,3,4,5,6];
let num=0;
let result=arr.reduce(function(prev,next){
  //上一个默认是数组中的第一项，下一个默认是数组的第二项
  //上一个变成第一次返回的结果，下一个就是第三项
  console.log(prev,next);
  return  prev+next;
});
console.log(result);
```
### 把二维数组变为一维数组
```
let arr=[['北京'],['上海'],['广州']]；
let result=arr.reduce(function(prev,next){
//prev['北京']next['上海']
//prev['北京','上海']next['广州']
 return prev.concat(next);
});
console.log(result);
```
### MVC
- M model  数据
- V  view  视图
- C controller 控制器
> 当用户改变页面是，会触发控制器，控制器会调用数据，将数据展示到对应的视图上（单向的） V -> C -> M -> V
### MVVM
- M model  数据
- V view 视图
- VM viewModel  视图模型 所有数据都挂在viewModel上
> 先将数据绑定在视图上，会监听视图的改变，视图改变后会触发数据的变化，这种实现是通过viewModel
### vue的指令
### v-model
- 双向绑定 v-model可以将数据绑定到视图上，当视图改变时，可以将数据更改
- 只有表单元素可以更改视图，input、  radio、 checkbox、 select 、textarea只有以上5个可以增加v-model指令，其他均不行，只能放置表达式
```
<input type="text" v-model='message'>
```
### v-html
> 将字符串展示成html
```
<div id="app">
 <div v-html='html'></div>
</div>
<script>
  let vm=new Vue({
    data:{
    html:'<h1>hello world</h1>';
}
  })	
```
### v-once
> 只让数据绑定一次 在数据更新后不再刷新视图
### v-text
> 用法和{{}}一样，优点：不会闪烁
### v-for循环
- 变量用{{}}输出 普通html不用包在{{}}中
- v-for可以遍历数组，字符串，对象
- 循环数组，要循环谁就在谁的身上写v-for，可以使用for  in或者for  of
- 遍历字符串
- 遍历对象 对象没有索引
### events事件
- v-on代表的是指令可以用来绑定事件，绑定时间执行括号不需要传递参数则不加，如果写()需要手动传入事件源$event
- v-on过长可以简写成@符
- v-show 操作的是css样式，如果不满足条件则display：none
- v-if 它操作的是dom元素，默认不满足条件时dom不存在，满足后则增加dom元素
- 频繁操作显示和隐藏，使用v-show
### 在事件执行时判断keycode进行操作
- 方法中应该放的是纯逻辑内容，不包含判断

### 修饰符 修饰一些内容
方法名.修饰符

### vue vue-resource(ajax)
- 安装vue和vue-resource和bootstrap
```
npm install vue vue-resource bootstrap  --save
```

### 修饰符
- .stop 阻止冒泡事件（停止向上传递）
- .capture 增加给父级的让事件从外到内执行，会发生冒泡事件
- .self 由自己触发，不包括自己的子集
- .once 只绑定一次事件（在执行事件后移除事件）
- .prevent 阻止默认行为
- .code 根据键盘码触发事件 .enter、.space、.delete...

### 绑定动态属性
- 动态属性用v-bind绑定,可以简写成":"
- 在绑定动态属性中有两个特殊class，style
### class
- 对象绑定
```
.a{background:'red'}
.b{color:'green'}
<div :class="{a:flag,b:flag1}"></div>
data:{
 flag:true,
 flag1:true
}
```
- 数组绑定
```
.a{background:'red'}
.b{color:'green'}
<div :class="[c1,c2]"></div>
data:{
 c1:'a',
 c2:'b'
}
```
### style样式绑定
```
<div :style="[s1,s2]"></div>
data:{
s1:{ backgroun:'red'},
s2:{color:'red'}
}
```
### 生命周期
- 针对的是组件，根组件也是组件，仍然遵循这个流程
### vue组件的几种方法
```
beforeCreate(){alert('创建之前')},//一般不使用
created(){alert('创建完成')},//创建完成后可以获取数据
beforeMount(){alert('开始挂载')},
mounted(){alert('挂载完成')},//在mounted中也可以获取数据
//数据更新就会调用这两个函数  拦截
beforeUpdate(){alert('开始更新')},
updated(){alert('更新之后')},
beforeDestroy(){alert('销毁之前')},
destroyed(){alert('销毁之后')},
```
### computer
> 计算 “属性”不是方法，可以根据已有属性推断出一个新的属性来
> 时刻监听数据的变化只要有数据变，不管和sum函数有没有关系都会执行
### watch、computed、methods的区别
- 如果简单的逻辑首先要想到watch，如果是复杂的用computed，如果是异步并且有“中间过程”用watch
- methods 触发的函数
- computed 计算的函数  不能处理yibu













