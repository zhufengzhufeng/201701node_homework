## React
- React是一个用于构建用户界面的库
- React元素：虚拟DOM(它是用来描述真实DOM结构，最终会由ReactDOM把虚拟DOM转成真实DOM)
- 标签如果是小写字母开头的话，那么它就是一个React元素，就会把它转成真实的DOM元素并插入到root内部
```
import React from 'react';
import ReactDOM from 'react-dom';
ReactDOM.render(<h1 style={{backgroundColor:'red'}} className="green">hello</h1>,document.querySelector('#root'));
```
#### Each child in an array or iterator should have a unique "key" prop.
```
let names = ['大毛','2毛'];
{/*
<ul>
    <li>大毛</li>
    <li>二毛</li>
    <li>三毛</li>
</ul>*/}
import React from 'react';
import ReactDOM from 'react-dom';
ReactDOM.render(
    <ul>
        {
          names.map((name,index)=>(
              <li key={index}>{name}</li>
          ))
        }
    </ul>,document.querySelector('#root')
);
```
## 定义组件 两种方式:Function Class
- 一个组件需要有属性和状态，属性用来存放那些由父组件传入的，自己不能改变的数据；状态是组件内部初始化，而且只能由内部修改
- 函数定义组件
```
function Person(props){
  return (
      <div>
          <p>姓名:{props.name}</p>
      </div>
  )
}
let p={age:8,name:9};
ReactDOM.render(<Person {...p}>,document.getElementById('root'));
```
- 类定义组件
```
class Person extends React.Components{
    constructor(props){
        super(props);//this.props=props;
        //这种给状态赋值的方式只能在构造函数中初始的时候用
        this.state={happy:true};
    }
}
```
- 在组件的方法里，只有constructor render还有其它的生命周期函数里面的this指向当前组件的实例，除此以外其它方法里的this都指向undefined，所以需要手工绑定this
- 手动绑定this,1,在绑定的时候bind this 2,在绑定的时候用箭头函数 3，在定义的时候用箭头函数
```
class Person extends React.Components{
    constructor(props){
        super(props);
        this.state={happy:true};
    }
    changeHappy=()=>{
        this.setState({
            happy:!this.state.happy
        })
    }
    render(){
        return (
            <div>
                <p>姓名:{this.props.name}{this.state.happy?'开心':'伤心'}</p>
                <button onClick={this.changeHappy}>改变</button>
            </div>
        )
    }
}
```
## React.Children.map是react提供一个工具方法，用来实现针对可能是对象也可能是数组的映射
```
function Message(props){
    return (
        <ul>
         {
            React.Children.map(props.children,(item,index)=>(
                <li key={index}>{item}</li>
            ))
         }
        </ul>
    )
}
ReactDOM.render(<Message>
                    <span>2毛</span>
                </Message>,document.querySelector('#root');

)
```
## lifecycle
- 1,实例化组件类，并调用它的render方法得到虚拟DOM
- 2,React将要把此虚拟DOM元素挂载在页面中
```
import React from 'react';
import ReactDOM from 'react-dom'
export default class Counter extends React.Component{
    constructor(props){
        super(props);
        this.state={number:0};
    }
    componentWillMount(){
        console.log('1. componentWill 组件将要被挂载')
    }
    componentDidMount(){
        console.log('3, componentDidMount 组件挂载结束')
    }
    handleClick=()=>{
        this.setState({number:this.state.number+1});
    }
    //组件是否应该更新
    shouldComponentUpdate(newProps,newState){
        console.log('4, shouComponentUpdate 组件是否要被更新');
        if(newState.number%2==0){
            return true;
        }else{
            return false;//如果返回false render方法将不再执行
        }
    }
    componentWillUpdate(){
        console.log('5, componentWillUpdate 组件将要更新');
    }
    componentDidUpdate(){
        console.log('6, componentWillUpdate 组件更新完成');
    }
    componentWillUnMount(){
        console.log('7, componentWillUnMount 组件将要被卸载')
    }
    render(){
        console.log('2, render渲染');
        return(
            <div>
                <button onClick={this.handleClick} className="btn btn-primary">父计数器<span className="badge">{this.state.number}</span></button>
            </div>
        )
    }
}
```

