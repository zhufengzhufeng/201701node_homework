
### Vue中的修饰符 （可以修饰一些内容）
- @方法名.修饰符
- .stop 阻止冒泡事件（停止向上传播）
- .capture增加给父级的让事件从外到内执行，会发生冒泡事件（先捕获再冒泡）
- .self由自己触发，不包括自己的子集
- .prevent 阻止默认行为
- .once 只绑定一次事件（在执行事件后移除事件）
- .code根据键盘事件码触发事件
### 绑定动态属性
- 动态属性由v-bind绑定，可以简写成：
- 在绑定动态属性中有两个特殊class，style
#### class
- 对象绑定
```
//CSS部分
.a{background:'red'};
.b{color:'green'};
//HTML部分
<div :class="{a:flag,b:flag1}"></div>
//JS部分
data:{flag:true,flag1:ture};
```
- 数组绑定
```
//CSS部分
.a{background:"red"}
.b{color:"green"}
//HTML部分
<div :class="[c1,c2]"></div>
//JS部分
data:{c1:'a',c2:'b'}

```
#### 样式绑定
```
//HTML部分
<div :style="[s1,s2]"></div>
//JS部分
data:{s1:{background:'red'},s2:{color:'red'}}

```

### vue-resource（ajax）
- 安装vue和vue-resource
```
npm install vue vue-resource --save
```

### 生命周期
- 针对的是组件，根组件也是组件，仍然遵循这个流程。vue在组件中的每个环节都提供了钩子函数。
- 当调用vm.$mount()挂载后执行挂载数据
- 当调用vm.$destroy()后执行删除实例
![Alt text](./lifecycle.png)

- 生命周期的方法有哪些
```
beforeCreate(){},//一般不使用
created(){},//创建完成后，可以获取数据
beforeMount(){//开始挂载},
mounted(){//(挂载结束)在mounted中也可以获取数据}
beforeUpdate(){//('开始更新')更新和拦截。数据更新就会调用这两个函数}
updated(){//(('更新完成'));}
beforeDestroy(){//('开始销毁')}
destroyed(){//('销毁完成')}
```
-  

```
  vm.$mount('.app');//等价于el:'.app';
  vm.$destroy();
  vm.$data;//就是我们在data里边写的对象
  vm.$options.message;//在实例上自定义数据，没有放在data中。
 /*所有带有$的，都是Vue的内部属性，是vue提供的*/
```