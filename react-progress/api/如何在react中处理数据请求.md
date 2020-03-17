# 如何在react中处理数据请求 ？
数据层是必不可少的，在react中你可以很灵活地处理你的数据。  

### 在组件内部处理
在组件内处理数据请求，通常适用于那些简单而不复杂的应用。   
##### 1，class组件  
在class组件内处理数据请求的话，通常需要在`componentDidMount`生命周期方法内处理。

下面是一个例子：
```js
class App extends React.Component {  
    
    // 1，声明初始state
    state = {
        data: null
    }
    
    // 2，请求并更新数据
    componentDidMount(){
        // ...ajax请求...
        // 更新数据
        if(data){
            this.setState({ data });
        }
    }

    render(){
        // 3，渲染数据
        const { data } = this.state;
        return (
            <div>
                { data }
            </div>
        )
    }
}  
```

##### 2，函数组件    

函数组件本身没有生命周期，但是我们可以借助`react hook`中的`useEffect`来处理数据请求。

函数组件的`useEffect`相当于class组件的`componentDidMount`。
```js
import React,{ useState, useEffect } from 'react';  

export default () =>{     

    // 1，声明初始state
    const [ data, setData ] = useState(null);
    
    // 2，请求并更新数据
    useEffect(async ()=>{
        // ...ajax请求...
        // 更新数据
        if(result){
            setData(result.data);
        }
    })
   
    // 3，渲染数据
    return (
        <div>
            { data }
        </div>
    )
}
```

### 在组件外部处理

在react中，数据也是一种`state(状态)`。

使用react做开发，通常中大型复杂应用都需要用到第三方状态管理器，比如redux、mobx、dva等等。

而这些状态管理器相应地拥有非常强大的数据管理能力，于是通常组件的数据层交由这些状态管理器来管理。

以`dva`为例，`dva`提供了一个`model`模块专门用于处理组件外部状态的(含数据层)。  

下面是一个案例，使用`dva`来管理`用户信息`数据，我们来看`dva`是如何管理这些数据的：  

1，添加数据请求函数：
```js
// 请求函数 - 请求用户信息
const fetchUser => () =>{
   return fetch("/api/user").then(res=>res.json());
}
```
2，dva 的 `model层`中处理数据请求和更新：
```js
app.model({
  namespace: 'usermodel',
  state: {
    user: null
  },
  // effects为副作用，专注于数据处理
  effects: {
    *getUser(action, { call, put }) {
      //1， 调用fetchUser请求函数，向后台请求用户数据
      const user = yield call(fetchUser, 1000);
      //2， 更新user
      yield put({ type: 'updateUser',payload: { user }})
    },
  },
  reducers: {
    updateUser(state,action) {
      //3， state为旧的state，这里被新的state覆盖
      return { ...state, ...action.payload };
    },
  },
  subscriptions: {
    // 订阅
  },
});
```
3，dva的state同步更新到react组件
```js
// dva 的 connect 方法可以将组件和数据关联在一起
import { connect } from 'dva';  

// MyComponent为react组件，通过connect方法从dva里面获取最新的state。
connect((state)=>{
   return { user: state.user }
})(MyComponent);
```

4，react组件：  
```js
class MyComponent extends React.Component {

    componentDidMount(){
        // 触发action - "getUser"(model - effects - getUser)
        this.props.dispatch({ type:"getUser" });
    }

    render(){
        // 从dva中获取的最新state - user
        const { user } = this.props;
        return (
            <div>
                当前登录的用户是：<b>{ user && user.name }</b>
            </div>
        )
    }
}
```
