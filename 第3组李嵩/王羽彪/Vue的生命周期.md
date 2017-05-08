---
title: '''Vue的生命周期'''
date: 2017-05-06 19:24:33
tags:
 - vue
 - vue之生命周期
---
## 生命周期
- vue在组件的每个环节都提供了钩子函数(回调)
> 当调用vm.$mount()挂载后执行挂载数据
> 当调用vm.$destroy()后执行删除实例
### 图示
![vue声明周期图解](../img/lifecycle.png)
### 8个状态
```$xslt
let vm =new Vue({
    el:'#app',
    data:{
        msg:data
    },
    beforeCreate(){
        alert('开始创建前触发')
    },
    created(){
        "use strict";
        alert('创建完成时触发')
    },
    beforeMount(){
        "use strict";
        alert('挂载之前')
    },
    mounted(){
        "use strict";
        alert('挂载完成后')
    },
    beforeUpdate(){
        "use strict";
        alert('更新之前')
    },
    updated(){
        "use strict";
        alert('更新完成')
    },
    beforeDestroy(){
        "use strict";
        alert('销毁之前')
    },
    destroy(){
        "use strict";
        alert('销毁完成')
    }
});

```


