title: 小解redux
tags: []
categories: []
date: 2017-08-08
---
[官方文档](https://facebook.github.io/react/docs/react-component.html) [生命周期推荐文档](https://developmentarc.gitbooks.io/react-indepth/content/life_cycle/introduction.html)
##### 初始化组件流程 #####
>es5：                     
getDefaultProps                
getInitialState         
componentWillMount         
render                  
componentDidMount

>es6：
defaultProps
state
componentWillMount
render
componentDidMount

###### getDefaultProps ######
初始化props
```javascript
//es5 写法
export default React.createClass({
  getDefaultProps:function(){
    return {
      //... props
    }
  }
})
//es6 写法
export default class MyComponent extends React.Component {
  static defaultProps={
    //... props
  }
}
```
###### getInitState ######
初始化state
```javascript
export default React.createClass({
  getInitialState:function(){
    return {
      //... state
    }
  }
})
//es6 写法
export default class MyComponent extends React.Component {
  constructor(){
    super(props)
    this.state={
      //...state
    }
  }
}
```
###### componentWillMount ######
挂载前执行的函数
```javascript
export default React.createClass({
  componentWillMount:function(){
    // do something
  }
})
//es6 写法
export default class MyComponent extends React.Component {
  componentWillMount(){
    //do something
  }
}
```
###### render ######
dom的生成和挂载
```javascript
export default React.createClass({
  render:function(){
    // do something
    return <Element/>
  }
})
//es6 写法
export default class MyComponent extends React.Component {
  render(){
    //do something
    return <Element/>
  }
}
```
###### componentDidMount ######
组件挂载后执行，一般初始化ajax数据在此处请求，如果在componentWillMount中运行ajax去改变state等，有可能在关联的子组件上会出现报错现象，据说在下一代的fiber中还会引发运行流程混乱
```javascript
export default React.createClass({
  componentDidMount:function(){
    // dom已经生成，可以操作元素
    // do something
  }
})
//es6 写法
export default class MyComponent extends React.Component {
  componentDidMount(){
    // dom已经生成，可以操作元素
    //do something
  }
}
```

##### 更新组件流程 #####
>componentWillReceiveProps
shouldComponentUpdate
componentWillUpdate
render
componentDidUpdate

###### componentWillReceiveProps ######
组件即将接收props，父组件更新或者自己更新都会运行此函数。默认情况比如props中含有array，父组件更新时对array进行了push并不会更新子组件，子组件可以在componentWillReceiveProps中进行判断强制更新。
```javascript
//如使用es5 在内部切成对象function模式
componentWillReceiveProps(nextProps){
  //... 
  //this.forceUpdate() 相当于直接运行render函数
}
```
###### shouldComponentUpdate ######
判断组件是否更新，返回Boolean值，true更新，false不更新，在优化时，一般会引入immutable.js等进行props和state的判定。当然react也提供了一个React.PureComponent使用，但仅仅基于‘===’判断props和state的更新
```javascript
//如使用es5 在内部切成对象function模式
shouldComponentUpdate(nextProps,nextState){
  //... 
  if(...){
    return false
  }
}
```
###### componentWillUpdate ######
在render前执行的函数（why not run in render T_T,mybe first time mount not needed ^v^）
```javascript
//如使用es5 在内部切成对象function模式
componentWillUpdate(nextProps,nextState){
  //... 
}
```
###### render ######
与挂载一致
###### componentDidUpdate ######
组件已经更新完成，如需要使用原来的state和props再做一些活儿，可以在此处运行
```javascript
//如使用es5 在内部切成对象function模式
componentDidUpdate(prevProps, prevState){
  //...
}
```
##### 组件销毁 #####
>componentWillUnmount

###### componentWillUnmount ######
组件即将销毁，此处一般用来清理一些计时器、监听事件等
```javascript
//如使用es5 在内部切成对象function模式
componentWillUnmount(){
  //...
}
```