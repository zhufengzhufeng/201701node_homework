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
### vue-source
### 扩展
hash：保证再当前页面上 保证不跳转页面，并且更新url，获取hash值
window.location.hash