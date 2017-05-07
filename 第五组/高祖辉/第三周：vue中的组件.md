## vue中的组件
>- vue中的组件是自定的标签，可以扩展的原生html元素，封装可复用的代码 
>- note：
	1、在标签命中不要使用大写，标签名字必须用短横线隔开
	2、模板中只能有一个根元素，不能使用并列标签。
### 定义组件
>- 全局定义，在所有实例中都可以使用这个组件
```
	<template id='hello'>
		<div>
			<div>hello</div>
			<div>world</div>
		</div>
	</template>
	let data={msg:'world'}
	Vue.component('myComponent',{
	template:'#hello',//通过模板的ID来引用这个组件
	return {msg:'world'};//此时不能return data；这样会导致如果有多个实例运用这个组件会导致，三者共享同一个data，改变其中一个，会导致其他的都改变。对象变量会导致共享数据。
	})
此时就可以在实例中使用my-component标签。
```
>- 局部定义
```
let vm=new Vue({
	el:'#app',
	data:{msg:'hello'},
	components:{
		'my-component'(myComponent):{
		template:'<h1>{{msg}}</h1>',
		data(){
			return {msg:'world'};
			}
		}
	}
})
1、子组件不能直接使用父组件的数据
2、子组件可以声明自己的数据
```
### 组件之间的数据传递
	1、每个组件是没关系的，都应该产生自己的数据。在组件中data使用的方法和默认的vm一样。只是data不再是对象而是函数。组件可以无限嵌套。
	2、声明组件的名字，不能为已经存在的标签
	3、组件的嵌套，子组件必须写在父组建的模板中才能使用
>- 1、父级向子级传递数据（传递的属性值）

	1、如果直接写a='b'格式传递的是字符串，动态数据获取用的是v-bind，一般无论是动态还是静态，我们都会采用:。
	2、:msg='meat',meat是变量;msg='meat',meat是字符串，:msg="'meat'",meat是字符串
	3、子级不能直接改变父级的数据，如果要修改可以将父级的数据修改后赋值给子级的变量，可以使用data或者computed
```
<div id=app>
	<child :data='aaa' :data1="bbb"></child>
	//此处，在子组件中左边的是子组件的接收,用props接收,如果是放在数组中每一项就是一个字符串,右边是从父级传递的数据。
</div>
<script>
	let vm=new Vue({
			el:'#app',
			data:{
			aaa:'xxxxx',
			bbb:'yyyyy'
			}
			components:{//
				child:{
				props:['data','data1']，
				template:'<div>{{msg}}</div>',
				data(){
					return {msg:this.data+'zxvv'}
					}，
				computed：{
					msg:{
						get(){
						return  this.data+'zxvv'
							}
						}
					}
				}	
			}
		})
</script>
```
`props`中的`validate`：

	1、props：['xx','yy','zz'];
	2、props：{
		aa:{
			type:[Number,String],//选择值得类型符不符合要求
			default:'acac',//默认值
			validator(val){//校验函数
				return val>200//返回false，校验失败。
			}
			required：true，//代表属性必须填		
		}
	}
>- 2、子级向父级传递数据（借助于事件）

	1、子级$emit后会触发自己身上的某一个自定的方法，这个方法对应的函数在父级的身上。
```
<div id="app1">
    {{datas}}
    <child @get-data="getData"></child>//自定义方法写在自己身上，右边的是父级对应方法的函数
</div>
let vm1 = new Vue({
        el: '#app1',
        data: {
            datas: '',//用来接收自己传递的空数据
        },
        methods: {
            getData(msg){//接受的参数就是从子级传递过来的数据
                this.datas = msg;
            }
        },
        components: {
            child: {
                template: `<div><button @click="say">{{msg}}</button></div>`,//绑定触发事件
                methods: {
                    say(){//触发事件，以及自定义方法
                        this.$emit('get-data', this.msg);//这里的this指的是当前子组件
                    }
                },
                data(){
                    return {
                        msg: 'xxx'
                    }
                }
            }
        }

    })
```
>- 3、兄弟之间传递数据
	
	1、兄弟之间传递数据需要借助于事件车，通过事件车的方式传递数据eventBus
	2、创建一个Vue的实例，让各个兄弟共用同一个事件机制。
	3、传递数据方，通过一个事件触发bus.$emit(方法名，传递的数据)。
	4、接收数据方，通过mounted(){}触发bus.$on(方法名，function(接收数据的参数){用该组件的数据接收传递过来的数据})，此时函数中的this已经发生了改变，可以使用箭头函数。
### slot
	具名slot，通过组件传入模板，每个模板指定是slot名字，这个名字和定制模板匹配到，会替换定制的模板。
	slot是vue中提供的一个标签，用来做模板定制的。属性，事件，定制模板组成了组件的API。
	**使用slot分发内容**
	为了让组件可以组合，我们需要一种防暑混合父组件的内容与子组件自己的模板。这个过程被称作内容分发（transclusion），vue.js实现了一个内容分发API，使用特殊的<slot>元素作为原始内容的插槽。
	**编译作用域**
	 父组件模板的内容在父组件作用域内编译；子组件模板的内容在子组件作用域内编译。
	 **单个slot**
	 除非子组件模板包含至少一个 <slot> 插口，否则父组件的内容将会被丢弃。当子组件模板只有一个没有属性的 slot 时，父组件整个内容片段将插入到 slot 所在的 DOM 位置，并替换掉 slot 标签本身。
	 最初在 <slot> 标签中的任何内容都被视为备用内容。备用内容在子组件的作用域内编译，并且只有在宿主元素为空，且没有要插入的内容时才显示备用内容。
	 **具名slot**
	 <slot>元素可以用有个特殊的属性name来配置如何分发内容。多个slot可以有不同的名字。具名slot将匹配内容片段中对应slot特性的元素。但任然可以有一个匿名slot，它是默认的slot，作为找不到匹配的内容片段的备用插槽。如果没有默认的slot，这些找不到匹配的内容将被抛弃。
### 递归组件
	组件在它的模板内可以递归地调用自己。recursive 递归组件，自己调用自己，必须有中断条件。
	默认情况下，递归组件是不会执行的，要制定name属性(只在局部组件中需要添加)，全局逐渐不需要加name属性。
### 动态组件
	is可以指定当前标签内可以指定插入什么元素,可以防止解析出错。
	radio中默认没有绑定数据，要给value值，这个value值会映射到radio上
```
<keep-alive>
    <component :is="rad"></component><!--缓存组件的上一次状态,防止每次切换时都需要渲染组件-->
</keep-alive>
```
		 