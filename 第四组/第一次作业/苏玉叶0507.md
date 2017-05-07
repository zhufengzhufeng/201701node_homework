####路由定义
> 1. 单页web应用，就是只有一张web页面的应用，是加载单个HTML页面并在用户与应用程序交互时动态更新该页面的web应用程序
> 2. 不切换页面，还可以展示不同内容
>  - hashchange->hashHistory
>  - pishState->browserHistory->history
#### vue-router介绍
>可以配置组件和路由映射，可以使Vue.js+vue-router创建单页应用

#### vue-router 安装
>1. 初始化 npm init -y
>2. 安装 npm install vue-router --save
>3. 安装 npm install vue vue-router bootstrap animate.css --save(组合安装，包含bootstrap框架和animate动画)

####初探vue-router
>默认配好的映射组件会加载到router-view中，可以使用router-link进行页面跳转
```
  <router-link to="/meat">猪肉</router-link>
  <router-link to="/greens">蔬菜</router-link>
  <router-view></router-view>
```

####路由参数
> vue-router提供了一个$route对象，如果要获取路径传递参数，数据会全部存放在params对象中
> 1. 例如匹配的路径/drink/type/3  匹配的规则/drink/type/:id  ,会自动形成一个属性为params的对象params:{id:3}
> 2. 因为路由已经被注入到vm中，this.$route(这里存放的是路由的信息),this.$router(这里存放的是路由的方法 )

#### 路由跳转
>  1. 跳转新的路由（会产生历史纪录）    
>    - router.push({path:'/foods/fruit',query:{name:1}})
>  2. 替换当前的路由并跳转（不会产生历史纪录）
>    - router.replace('/foods/fruit')
>  3. 重定向路由 {path:'*',redirect:'/home'}
>    - 路由是从上到下匹配的到最下面的时候都没有匹配到，会走到*（匹配所有，当你访问不存在的路径的时候），会跳转到/home上 
####监控路由变化
>   全局监控router.beforeEach(to,from,next)当路由切换的时候，会触发这个函数，范围最大，任何路由切换都会触发这个函数
>    - 参数to:去到哪个路由
>    - 参数from:从哪个路由来
>    - 参数next:是否决定继续执行，是一个函数，如果调用next()表示继续，否则卡在这里不动
>      - 用户场景：可以校验是否登录成功，成功则继续，否则跳转到登录页
>      - next中可以传递参数，表示去哪
```
 router.beforeEach((to,from,next)=>{
        console.log(to)
//to是一个对象  Object {name: undefined, meta: Object, path: "/drink", hash: "", query: Object…}
        if(to.path=='/drink'){ //如果点击的是drink,让它跳转到food页面
            next({path:'/food'})
        }else {
            next()
        }
    })
```      
> 在组件中监控
```
beforeRouteEnter(to,from,next){
           console.log(100); //一般会在这个函数获取数据，不能使用this
           setTimeout(()=>{
               next(vm=>{
                   vm.message = 'world';
               }); //vm代表的当前实例
           },2000);
       }
```
> 不管能不能获取，都跳转页面
```
         mounted(){ //实例创建后，页面加载前
          setTimeout(()=>{
              this.message='world'},2000)
      }
```  

> 数据获取不到，不跳转页面     
     
```    
    beforeRouteEnter(to,from,next){//
    console.log(100)
    setTimeout(()=>{ //vm代表当前实例
      next(vm=>{vm.message='world'})
    },2000)
    }
```

####路由嵌套
>可以嵌套路由，可以指定父子关系，实现多router-view
>- 访问关系
>  1. 食物：猪肉，蔬菜 
>  2. 饮料：雪碧，酸梅汤

- 引入vue.js和vue-router.js
```
<script src="node_modules/vue/dist/vue.js"></script>
<script src="node_modules/vue-router/dist/vue-router.js"></script>
```
- 根组件
```
<div id="app">
    <!--当路由匹配到后，会将组件插入到router-view中-->
    <router-link :to="{path:'/food'}">食物</router-link><!--router-link:会自动转换成a标签-->
    <!--to="/home" 当点击首页的时候，会自动跳转到home路径，到对应的组件-->
    <router-link :to="{path:'/drink'}">饮料</router-link><!--会自动转换成a标签-->
    <router-view></router-view>

</div>
```
- food和drink模板
```
<template id="food">
    <div><!--根节点-->
        <div>食物</div>
        <router-link to="/food/meat">猪肉</router-link>
        <router-link to="/food/greens">蔬菜</router-link>
        <router-view></router-view>
    </div>
</template>
<template id="drink">
    <div><!--根节点-->
        <div>饮料</div>
        <router-link to="/drink/type/1">雪碧</router-link><!--写上/表示相对于根路径-->
        <router-link to="/drink/type/2">酸梅汤</router-link>
        <router-view></router-view>
    </div>
</template>
```
- js逻辑部分

```
<script>
    //默认页面首页router-view是空的，解决方法：1）配置一个默认页面 2）直接跳转到食物路由上
    var food={template:'#food'}
    var drink={template:'#drink'}
    var type={
//获取路由的信息，因为路由已经被注入到vm中，this.$route(这里存放的是路由的信息   this.$route.params.id
// 匹配的路径/drink/type/3  匹配的规则/drink/type/:id  params:{id:3}
//this.$router(这里存放的是路由的方法 )
       /* 计算id值的第一种方法  在当前页面的话去掉this  取的id值就是$route.params.id
        template:'<div>当前种类是第{{$route.params.id}}个</div>',
        mounted(){
            console.log(this.route)
             }*/
       //第2种方法 用计算属性计算出来
        template:'<div>当前种类是第{{id}}个</div>',
        computed:{
            id(){
                return this.$route.params.id
            }
        }

    }

    const routes=[
        {path:'',component:{template:'<div>这是默认吃的内容。。。。。</div>'}},//path:路由
        {path:'/food',
            component:food,
         children:[//子路由不能写/，/代表的是根路径
             {path:'meat',component:{template:'<div>food</div>'}} ,
             {path:'greens',component:{template:'<div>greens</div>'}}
         ]
        } , //首页对应的组件
        {path:'/drink',component:drink,
            children:[  //id这个值必须要有，但是可以随机 /drink/type:1   params:{id:1}
                {path:'type/:id',component:type}
            ]
        }, //维护页面
        {path:'*',redirect:'/food'}//路由是从上到下匹配的到最下面的时候都没有匹配到，会走到*（匹配所有，当你访问不存在的路径的时候），会跳转到/food上      redirect：重定向
    ] //构建路径映射表   默认是hash  #/home
    var router=new VueRouter({
        mode:'history', //默认路径是  localhost:63342/food
        //变成浏览器管理历史纪录 路径不再是#/food,不能直接刷新浏览器，因为页面不存在，服务端需要提供支持
        routes:routes //key的名字是固定的
        //router(在页面任何地方都可以使用)=this.$router（在组件中使用）
    })
    var vm=new Vue({
        el:'#app',
        router:router  //key的名字是固定的
    })
</script>
```
