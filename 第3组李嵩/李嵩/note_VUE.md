### MVC
m-mode v-viw c-controller 模型视图控制器,控制器调用数据，数据展示到对应的视图
### MVVM
m-mode v-viw vm-viewModel
采用双向绑定（data-binding）：View的变动，自动反映在 ViewModel，反之亦然。Angular 和 Ember 都采用这种模式。
### vue
vue的js包，有压缩和不压缩版本，压缩版本不会警告。一般开发时选择未压缩版
### vue的生命周期
beforeCreate-->created-->beforeMount-->mounted-->beforeUpdate-->updated-->beforeDestroy-->destroyed
```javascript
//hooks
var vm = new Vue({
//el:'#app' 等同于$.mount('#app')
beforeCreate(){},//基本不使用
created(){},
beforeMount(){},
mounted(){},//获取数据
//更新  拦截会调用这俩函数
beforeUpdate(){},
updated(){},
//调用vm.$destroy();$为vm自身的属性，可用vm.$data，vm.$options.attr：获取实例自定义属性
beforeDestroy(){},
destroyed(){}
})
```
### 常用指令
1. v-model
双向数据绑定，表单元素上使用，将数据绑定再表单元素上，如果表单内容更改会导致数据变化
2. v-html
将字符串的html转为html
3. v-once
数据绑定一次，随后数据变化不更新视图变化
4. v-text
同{{}}用法一致，绑定数据显示再视图，防止单个元素闪烁
5. v-for
循环数组/对象/字符串，语法是v-for(value of/in items|(value,index) of items);
6. v-on
绑定事件语法：v-on：事件名='函数名()|简写为\@'；函数写在vm中，methods{函数名（）{}}
7. v-show|v-if..v-eles-if..v-else
控制元素显示和隐藏，show控制样式，其他控制dom元素
8. v-bind
 - 动态获取数据，v-bind:title='attr',可以简写成：title='attr';
 - ！！动态绑定class比较特殊，与原生class可以共存，动态覆盖静态
   <div class="bg" :class="{font:true}">背景</div>
   <div class="bg" :class="[b,c]">数组</div>,数组绑定比较灵活，可以再里面直接加入项，'.class'Or'{font:true}'
 - 绑定行内样式
    尽量用class，用的比较少
### 修饰符
1. 按键修饰符
 - \@keyup.enter表示回车抬起事件，同时也可以用keyCode替代，写为@keyup.13
2. 事件修饰符
 - @click.stop|@click.capture,分别为组织冒泡和增加捕获，分别给子元素和父元素
 - @click.self,只有点自己的时候才执行，不参与其他元素的捕获和冒泡
 - @click.prevent,阻止默认
 - @click.once,只绑定一次事件，完成后移除事件
### computed
通过get/set方法实现双向操作，但其为同步，无法实现异步操作,适合做复杂逻辑，简单的给watch
```javascript
var vm = new Vue({
computed: {
             sum: {
                 get(){
                     //如果price和count变化会导致sum变化
                     return this.price * this.count;
                 },
                 set(val){
                     this.name = val;
                     //sum变化可能会改变name变化
                 }
             }
             }
});
```
### watch
异步事件触发某件事情时使用watch
```javascript
var vm = new Vue({
    data:{message:'hello',content:''},
    watch:{
        message(next,pre){//next新值，pre旧值
            this.content = '等待中';
            setTimeout(function() {
              vm.content = next+'ls';
            },2000);
        }
    }
})
```
### Vue.component
组件一般有3部分组成，模板/slot /属性
1. 全局注册组件
```javascript

Vue.compoent('myComponent',function() {
  template:'<div>Hello</div>'//必须有template属性以便渲染，且根元素只能有一个（template:'<div></div><div></div>'！错的）
  
});
```
```
<!--//如果模板太大，标签太多，vue允许再外声明一个template标签，全局组件-->
<template id='tem'>
    <div>
        <div>hello</div>
    </div>
</template>
.//通过模板的id可以引用js中调用
template:'#tem'
```
2. 局部组件(父子组件)
首先，组件的声明不能与已存的html标签重复
vue 的组件同vm相同有自己的声明周期和自己的各种属性，不同点在于，子组件的data需要使用函数声明。

```javascript
//只是再声明的时候有区别
var vm = new Vue({
        el: '#app',
        components:{
            'my-com1':{
                template:'#com'
            }
        }
    })
//如果局部子组件想使用父的属性或方法时，可以再自组件中自己定义数据,可以声明多个子组件，但其自己的数据不要互相污染。
var vm = new Vue({
        el: '#app',
        data:{
            msg:'hello'
        },
        components:{
            'my-com1':{
                template:'<h1>{{msg}}</h1>',
                data(){//子组件定义数据必须是函数类型
                    return{msg:'world'}
                }
            }
        }
    })
```
另外，vue的组件可无限嵌套
```javascript
var vm = new Vue({
        el: '#app',
        data: {msg: 'hello'},
        components: {
            'my-com1': {
                template: '<h1 @click="change">{{msg}}<my-com3></my-com3></h1>',
                data(){//自组件定义数据必须是函数类型
                    return data;
                },
                components:{
                    'my-com3':{
                        template:'<h3>lily</h3>'
                    }
                }
            }}});
                       
```
3. 父子组件数据传递
```vue
<div id="app">
    <child :data="meat" :vegetable="vegetable"></child>
</div>
    <script>
        var vm = new Vue({
            el:'#app',
            data:{
                meat:'五花',
                vegetable:'蔬菜'
            },
            components:{
                child:{
                    props:['data','vegetable'],
                    template:`<h1>切{{data}},吃{{vegetable}}</h1>`
                }
            }
        })
    </script>
```
4. 子组件校验父组件数据
此时只需要修改下props即可

```vue
 props:{
  msg:{},
  vegetable:{},
  c:{type:[Number,String],default:11,required:true},//type 数据符合的类型，default 默认值，required true 属性必须传递
   // 自定义校验函数
    validator(val){
         return val>200;
     }
},
```
5. 子组件属性传给父组件
```vue
<div id="app">
    {{m}}
    <child @show-money="say"></child>
</div>
<template id="child">
    <div>
        {{money}}元
        <button style="display: block" @click="tell">
            我有多少钱
        </button>
    </div>
</template>
<script>
    var child = {
        methods: {
           tell(){
                this.$emit('show-money', this.money)//当前实例方法emit,将数据发射给父级
            }
        },
        template: '#child',
        data(){
            return {money: 100}
        }
    };
    var vm = new Vue({
        el: '#app',
        data:{m:''},
        components: {
            child
        },
        methods:{
            say(money){
                this.m = money;
                console.log(this.m);
            }
        }
    })
</script>

```
6, 兄弟组件之间数据传递
```vue
//开车
```
#### 插槽
slot，vue提供的标签，用来做模板定制
```vue
<div id="app" class="container">
    <alert>
        <div><i>错误</i><p>有bug</p></div>
    </alert>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        components: {
            alert: {
                template: `<div class="alert alert-info"><slot>只是一个警告框</slot></div>`
            }
        }
    })
</script>
```
复杂一些的，使用具名slot
```vue
<div id="app" class="container">
    <alert>
        <div slot="footer">这是弹框底部</div>
        <div><i>错误</i><p>有bug</p></div>
        <div slot="header">这是弹框的头部</div>
    </alert>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        components: {
            alert: {
                template: `<div class="alert alert-info"><slot name="header"></slot><slot>只是一个警告框</slot><slot name="footer"></slot></div>`
            }
        }
    })
</script>
```
7. is
可以控制层级，比如表格中使用
```vue
<div id="app">
    <table>
        <tr is="temp"></tr>
    </table>
</div>

<script>
    var vm = new Vue({
        el:'#app',
        components:{
            temp:{
                template:'<div>hello</div>'
            }
        }
    })
</script>
```

#### 递归组件
   默认情况下，递归组件是不执行的，要指定name属性
   ```vue
components: {
            tree: {
                name: 'tree',
                props:{'datas':{}},
                template: '<ul><li>{{datas.name}}<tree v-for="child in datas.children" :datas="child"></tree></li></ul>'
            }
        }
```

#### vue animation
- v-enter:过渡开始
- v-enter-active:激活
- v-leave:结束开始，一般不写
- v-leave-active：过渡动画结束
### vue-source
### 扩展
hash：保证再当前页面上 保证不跳转页面，并且更新url，获取hash值
window.location.hash
不切换页面，展示不同内容：pushState->browserHistory->history;hashHistorym