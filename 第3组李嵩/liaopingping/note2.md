###vue组件
1. 全局定义  全局定义的组件在任何实例的模板中都可以使用
```
<div id="app">
    <zf-component></zf-component>烤串命名
</div>
<script>
    var vm = new Vue({
        el:'#app'
    });
Vue.component('zf-component',{
    template:`<div>hello vuejs</div>`
});

</script>
<template id="hello">
    <div><!--这个模板里面也只能有一个根节点-->
        <div>hello</div>
        <div>hello</div>
    </div>
</template>
```

2. 局部定义:  在组件的实例中通过选项注册,只有在所注册的作用域中才能使用
```
<script>
    var vm = new Vue({
        el:'#app',
        components:{//有s
            'zf-component':{
                template:`<div>hello vuejs </div>`
            }
        }
    });
</script>
```

###组件的嵌套
```
<div id="app">
    <fruit></fruit>
</div>
<script>
    var vm = new Vue({
        components:{
            fruit 
        }
    });
    vm.$mount('#app');
    var fruit = {
      template:`<div>水果<sweet></sweet></div>`,
        components:{
          sweet//如果烤串形式的话,要加""
        }
    };
    var sweer = {
        template:`<div>甜的<waterMelon></waterMelon></div>`,
        components:{
            wateMelon
        }
    };
    var waterMelon = {
        template:`<div>西瓜</div>`
    };
```
</script>

###组件中的通信
父->子(属性):
```
<div id="app">
    <zf-component :language="language"></zf-component>
</div>

    var vm = new Vue({
        el:'#app',
        data:{
        language:'sdasd'
        },
        components:{
            'zf-component':{
                props:['language'],
                computed:{
                  l (){
                      return '加工后'+this.language;
                  }
                },
                data (){
                    return {
                        language: '加工后的'+this.language;
                    }
                },
                template:`<div>hello vuejs {{language}} </div>`
                components:{
                    anohter:{
                        props:[],
                                template:''
                    }
                }
            }
        }
    });
```


###校验获取到的数据
  ```
    props:{
          mag:{
              type:[Number,String]
              default:100,
              required:true,
              validator (value){
                  return value>100
              }
          }
      }
  ```
###子->父通信
$emit事件发射
```
<div id="app">
    <zf-component @custom-event="receive"></zf-component>
</div>

    var vm = new Vue({
        el:'#app',
        methods:{
          receive(data){
              console.log(data);
          }
        },
        components:{
            'zf-component':{
                template:`<button @click="run">发射</button>`,
                methods:{
                    run () {
                        this.$emit('custom-event','我好饿');
                    }
                }
            }
        }
    });

```

###平级之间的通信
on,emit
```
<script>
    var bus = new Vue();
    var vm = new Vue({
        el:'#app',
        created (){
            bus.$on('child',function (data) {
                console.log(data);
            });
        },
        component:{
            child:{
                data (){
                    return {child:'vue.js'}
                },
                template:`<div><button @click="up">ok</button></button></div>`,
                methods:{
                    up (){
                        bus.$emit('child',this.child);
                    }
                }
            }
        }
    });
</script>
<div id="app">
    <brother-one></brother-one>
    <brother-two></brother-two>
</div>
<script>
    var vm= new Vue({
        el:'#app',
        components:{
            brotherOne,
            brotherTwo
        }
    });
    var bus = new Vue();
    var brotherOne = {
        template:`<div>兄弟1<button @click="sendFood">给兄弟二送吃的</button></div>`
        data (){
            return {food:'meat'}
        },
        methods:{
            sendFood (){
                bus.$emit('送吃的',this.food);
            }
        }
    }
    var brotherTwo = {
        mounted (){
            bus.$on('送吃的',(data) =>{
                this.meat = data;
            });
        },
        template:`<div>兄弟2{{meat}}</div>`,
        data (){
            return {
                meat:'茄子'
            }
        }

    };
</script>
```


###slot插槽
```
<div class="alert alert-danger">

</div>
<div id="app">
    <alert>
        <div slot="footer">这是弹框的底部</div>
            <i>错误</i>
            <p>出BUG了</p>
        </div>
        <div slot="header">这是弹框的头部</div>
    </alert>
</div>
<script>
    var vm = new Vue({
        el:'#app',
        component:{
            alert:{
                template:`<div class="alert alert-danger">
                    <slot>这是一个alert弹框,</slot>
                    <slot name="header"></slot>
                    <slot name="footer"></slot>
</div>`
            }
        }
    });
</script>
```
###Buffer
1. 定义Buffer的三种方式:
new Buffer(size)
new Buffer(array)正常情况下是0-255
new Buffer(str,[encoding]);字符串建立
2. Buffer中常用的方法:
buffer.fill(0); 清零
buffer.write();
buffer.toString();
buffer.slice(0,4);
sourceBuffer.copy(targetBuffer,targetstart,sourcestart,sourceend);
3. 进制
(8).toString(2)) // "8" 十进制转2进制
parseInt("11", 2); // 2进制转10进制


###fs模块
同步读取readFile
异步读取readFileSync
创建目录: fs.mkdirSync('a/b/c/d');
判断一个文件是否存在: fs.exitsSync('./a');


