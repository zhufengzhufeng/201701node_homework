
###vue
<div id="app2">{{vm.message}}</div>
差值表达式除了直接写值外,不能写JS语法,但是可以赋值,运算,三元,或者展示放回结果
<div v-text="message"></div>可以避免小胡子闪烁
<div v-once="message"></div><!--数据只绑定一次,后续数据更改不影响这里-->
<div v-once>{{message}}</div>
<div v-html="message"></div><!--慎用,会自动将输入内容里面的标签识别,可能会导致代码注入-->
<input type="text" v-model="message"><!--双向绑定,只能放表达式,不能放三元等-->

##修饰符
@方法名.修饰符 比如@keyup.enter 当按键,并且是回车键的时候才触发这个函数
VUE不关心数据交互,如果要涉及到数据交互,就要用到vue-resource(ajax)
vue-resource不是vue自身的,是个第三方插件
npm install vue vue-resource bootstrap --save
按键修饰符:
.enter 回车 或者.13 任何关键字可以用对应keyCode去实现,记不住关键字就用keyCode去写
.space 空格
.left 左键 .right 右键
.esc 退出
.112是F1,但是要按住ctrl 再加F1
.65 键盘的a
修饰符可以连着写,比如这个a标签可以@click.self.prevent="Fn"这样去写
@.once事件只绑定一次@click.once这个事件只有效一次,当触发后就解绑

##在vue中事件的行为
  事件的行为有冒泡和捕获,默认是冒泡
  @事件.stop阻止冒泡,对应原生的e.stopPropagation();
  @事件.captrue捕获模式,把事件从冒泡模式变为捕获模式,要加在父级的
  @事件.self是只有在自己触发自己的的时候才执行,冒泡和捕获经过的都不会执行,即对捕获和冒泡免疫
  @事件.prevent阻止事件的默认行为

##v-bind
多个就用数组,有条件就用对象
<div :class="[b,c]"></div>
<div :class="[b,c,'box']"></div>
<div :class="[b,{font:flag},'box']"></div>
flag的指是通过后台动态设置的,所以动态属性的动态就是在可以改变上
数组和类名都不是独立的,如果数组里面某一个类名需要有条件,就把这个直接转换成对象,如果是很多都是有条件,则直接写对象,当flag值为true的时候,这个div才添加上font这个类名
<div :style="{background:'red',fontSize:'50px'}"></div>
<div :style="[s1,s2]"></div>

##computed
Computed是一个属性,不是一个方法

##watch
简单的计算,异步,定时器就要写在watch里面,数据的变化也写在watch里面

##生命周期
vm.$mount('.app);就相当于el:'.app'
vm.$destroy()销毁组件,就会触发对应的beforeDestroy,destroyed函数,销毁后数据不会再更新,但是之前写好的数据也不会消失
$的都是VM自己的属性,
vm.$data就是里面的data属性
```javascript
var vm = new Vue({
        breforeCreate(){
            //这些叫钩子函数
            alert( '创建之前');
            //不用这个函数,因为什么都没有
        },
        created (){
            alert( '创建完成');
        },
        beforeMount(){
            //小胡子挂载数据 ,就会触发这两个函数
            alert( '开始挂载');
        },
        mounted (){
            alert( '挂载完成');
        },
        beforeUpdate(){
            //如果我们修改挂载的数据就会触发这两个函数vm.msg = '';
            // 有改变就触发
            alert( '开始更新');
        },
        updated (){
            alert( '更新之后');
        },
        beforeDestroy(){
            //都是别人提供的方法,直接调用就可以了
            alert( '销毁之前');
        },
        destroyed(){
            alert( '销毁之后');
        }
        message:''
    });

```





