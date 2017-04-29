


## vue  vue-resource(ajax)
安装 vue  vue-resource
```
npm init
npm install vue vue-resource bootstrap --save

```

## 事件模型.stop .prevent .self .capture等修饰符可以累加使用
- 事件冒泡  事件捕获  阻止冒泡.stop  将事件模式变成捕获 .capture
- capture事件默认是双向的 先捕获 再冒泡 self只想点自己时触发 点别的 不触发

- @click.prevent  阻止默认跳转行为

## v-bind 简写为:   绑定[动态属性]
 v-bind:title="query"      :title="query"

- 动态绑定的class和原生的class 可以共存 如果覆盖问题,动态覆盖静态
- 对象绑定方式 :class="{样式:条件,样式:条件}"
- 数组绑定方式

## 修饰符
- .stop 阻止冒泡事件 (停止向上传递)
- .capture
- .self
- .prevent
- .once
- .code

## 绑定动态属性
- 动态属性用 v-bind 绑定 可以简写成 :
- 在绑定动态属性中有两个特殊的 class,style

### class
- :class
```
:class="{a:flag,b:flag1}"    //对象
:class="[className1,className2]"    //数组
```

- :style
```
:style:"[s1,s2]"

```

## 生命周期
- 针对的是组件,根组件也是组件