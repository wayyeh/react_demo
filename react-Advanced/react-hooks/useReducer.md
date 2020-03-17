# useReducer - 复杂的状态管理    

useReducer 是 useState 的变体，用于处理复杂的状态管理。

useReducer 可以作为 useState 的一种替代方案，它的灵感来自于redux的reducer。  

### 基本使用
useReducer主要接受三个参数，下面是useReducer的基本用法：  
```js
// useState基本用法
const [state, setState] = useState(initialState);  

// useReducer 基本用法
const [state, dispatch] = useReducer(reducer, initialState,initialAction);
```      
参数：    

> 1，reducer是一个函数，用于处理action并更新state   

> 2，initialState为初始的state    

> 3，initialAction为useReducer初次执行时被处理的action

返回值：    

> 1，state为状态    

> 2，dispatch为更新state的方法，它接受action作为参数    
    
<br/>

#### 如何用useReducer更新state ？   
只需要调用`dispatch(action)`方法即可更新state。 
```js
dispatch({ type: "reset" })
```
> dispatch用于更新state，当`dispatch(action)`被调用时，reducer方法也会被调用，并会根据action的描述去更新state。

<br/>

### reducer 参数详解 

在了解参数reducer之前，我们先来了解action是什么。

##### 1，action   

action是一种动作的描述，描述你发出的这个动作它应该做的事情。

action本质是一个对象(object)，它通常有一个`type`属性，用于描述该如何更新state，此外你还可以携带其他的参数。  

下面是action的一个例子：   

```js
const action = { 
    type: 'increment',  // 增量，表示该state的值要增加
    payload:{ 
        other: "value"  // 携带的其他参数
    } 
} 
```

我们该如何把描述性的action转换为最新的state ？这就是reducer函数所做的事情了。

##### 2，reducer   

reducer是redux的产物，它本质上是一个函数，主要用于处理action，并它返回最新的state。   

总的来说，reducer是action和state的转换器，它根据action的描述，去更新state。

它的结构如下：  
```js
(state, action) => newState
```

下面是reducer的一个应用案例：   
```js
const initialState = { count: 0 };  // 初始state

const reducer = (state,action) =>{  

    // 变量action，更加action的描述去更新state
    switch (action.type) {   

        // 当type为reset时，重置state的值，让state等于初始state
        case 'reset':    
            return initialState;  

        // 当type为increment时，让count加一
        case 'increment':
            return {count: state.count + 1};  

        // 当type为decrement时，让count减一
        case 'decrement':
            return {count: state.count - 1};    

        // 当type不属于上面任何一个时，不做任何更改，返回当前的state
        default:
            return state;
    }
}

const MyCompoent = () =>{

    const [state, dispatch] = useReducer(reducer, initialState);  

    return (
        <div>
            <p>当前count的值为：{ state.count }</p>
            <p><button onClick = {()=>dispatch({ type: 'reset' }) } >重置</button></p>
            <p><button onClick = {()=>dispatch({ type: 'increment' }) } >加一</button></p>
            <p><button onClick = {()=>dispatch({ type: 'decrement' }) } >减一</button></p>
        </div>
    )
}
```

### 结合useContext  

useContext可以解决组件间的数据共享的问题，而useReducer则解决了复杂状态管理的问题，因此把他们结合起来之后，我们就可以实现redux的功能了。那也意味着我们可以不再依赖第三方状态管理器。


