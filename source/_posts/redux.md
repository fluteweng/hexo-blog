title: 小解redux
tags: []
categories: []
date: 2017-08-07
---
[GitHub]("https://github.com/reactjs/redux")   [官方文档]("http://redux.js.org/docs/introduction/index.html")  [中文文档]("http://redux.org.cn/")

##### redux #####
redux是一个页面状态管理系统，可以看成是页面的数据存储，也是当前react的主流状态管理系统之一。由于在面对单页开发过程中，随着项目的逐渐变大，各页面间state的交互变得越来越复杂，为了保持良好的数据复用和页面间数据共享，引入一个状态管理系统有可能是一个比较好的选择。当然在引入redux后，数据操作也变得不如state那般直接。

redux由三部分构成：store、action、reducer

sotre：
  数据存储主体

action:
  操作触发器（必须为函数，返回值为一个对象，对象必须带有type属性）

reducer:
  操作函数对象

  ###### action ######
  首先来看action：
    ```javascript
    //定义action
    const action1 = function(){
      return {
        type: 'TYPE1'
      }
    }
    const action2 = function(data){
      return {
        type: 'TYPE2',
        data: data
      }
    }
    ```
  action是一个函数（这是规范），这个函数的返回必须有type属性，这是触发reducer工作的开关。当然在引入了异步，使用thunk等中间件时action函数内部会稍微有些小变动。

  ###### reducer ######
  再看reducer
    ```javascript
    const reducer = function(state={type1:null,type2:null},state){
      switch(action.type){
        case 'TYPE1':
          return state
          break
        case 'TYPE2':
          return Object.assign({},state,{type2:action.data})
          break
        default:
          return state          
      }
    }
    ```
  reducer是一个函数，第一个参数为state，第二个参数为action，在当前我们定义了2个action的type类型以及reducer收到2个type类型的处理方式，这个函数默认必须返回state

  ###### store ######
  store是由reducer生成的
  ```javascript
  import {createStore} from 'redux'
  const store = createStore(reducer)
  ```
  store 有3个方法
  store.getState()          获取store中数据
  store.dispatch(action)    启动action触发器，相当于调用reduer的相关case的执行
  store.subcribe(listener)  注册或者取消注册监听器

  ```javascript
  store.dispatch(action1)
  store.dispatch(action2('type2 data'))
  ```
  在dispatch一个action时候，store会执行reducer函数。如果多个reducer中含有相同的type，那么多个reducer相关代码都会得到执行。

  ###### combineReducers ######
  combineReducers是一个合并reducer的函数。当store数据越来越大时，如果一直加case，从代码的美观和合理性来说都是不可取的。combineReducers就是为定义多个reducer然后合并生成一个reducer而产生的。
  ```javascript
  import {combineReducers} from 'redux'
  const reducer1=function(state={},action){
    //...
    return state
  }
  const reducer2=function(state={},action){
    //...
    return state
  }
  const reduer = combineReducers({reducer1:reducer1,reducer2:reducer2})
  ```
  当然我们可以把结构处理的更为接近生产一些
  ```javascript
  //reducerGroup1.js 一般对应到某一使用state的模块名称
  const reducerGroup1 = {
    reducer1G1:(state,action)=>{
      //...
      return state
    },
    reducer2G1:(state,action)=>{
      //...
      return state
    }
  }
  export default reducerGroup1
  //reducerGroup2.js
  const reducerGroup2 = {
    reducer1G2:(state,action)=>{
      //...
      return state
    },
    reducer2G2:(state,action)=>{
      //...
      return state
    }
  }
  //reducer.js
  import reducerGroup1 from '/path/to/reducerGroup1'
  import reducerGroup2 from '/path/to/reducerGrop2'
  import {combineReducers} from 'redux'
  export cobineReducers(Object.assign({},reducerGroup1,reducerGroup2))
  //在实际使用中，不应该直接使用Object.assign，应该自己封装函数，对重名属性一些异常处理
  ```
##### react-redux #####
react-redux是个封装redux在react中使用的包，主要包涵两个部分
Provider:
  react组件的全局store载体
connect:
  对react相关组件传入需要的store属性和方法

  ###### Provider ######
  Provider只是一个载体，使用非常简单
  ```javascript
    import React from 'react'
    import {render} from 'react-dom'
    import {Provider} from 'react-redux
    import {createStore} from 'redux'
    import reducers from '/path/to/reducers'
    import App from '/path/to/App'
    let store = createStore(reducers)
    render(
      <Provider store={store}>
        <App/>
      </Provider>,
      document.getElementById('root')
      )
  ```

  ###### connect ######
  connect是连接store和react的components函数，使用十分频繁，可以说几乎是所有页面在使用。conncet使用格式connect(mapStateToProps,mapDispatchToProps)(MyComponent)
    MyComponent：需要store数据的react组件
    mapStateToProps：主要负责把store的数据以props的形式传给MyComponent
    mapDispatchToProps： 主要负责把store的action以props的形式传给MyComponent
  ```javascript
  import {connect} from 'react-redux'
  import MyComponent from '/path/to/MyComponent'
  import {actions} from '/path/to/actions'

  const mapStateToProps = (state)=>{
    return {
      property1:state.reducer1G1,
      property2:state.reducer2G1
    }
  }
  const mapDispatchToProps = (dispatch)=>{
    return {
      //定义需要处理store数据的函数
      handleComponentOperate1:(dispatch)=>{
        //给store dispatch一个action
        dispatch(actions.action1) 
      },
      handleComponentOperate2:(dispatch)=>{
        dispatch(actions.action2) 
      }
    }
  }
  const MyContainer = connect(mapStateToProps,mapDispatchToProps)(MyComponent)
  export default MyContainer
  ```
  当在react组件中调用this.props.handleComponentOperate1或者this.props.handleComponentOperate2时，store就会dispatch相关action更新数据，从而更新react相关组件props，起到更新dom的作用。