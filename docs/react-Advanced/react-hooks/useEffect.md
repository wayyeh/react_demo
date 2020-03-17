# useEffect - 副作用

数据获取、订阅、或手动修改React DOM这些行为都可以称之为`副作用(side effect)`。`useEffect`正是用来处理这些副作用的。

同时`useEffect`也是`componentDidMount`，`componentDidUpdate`，和 `componentWillUnmount`这几个生命周期方法的统一。

### 基本使用  
用法：
```js
useEffect(callback,array)
``` 
> 1，callback：回调函数，用于处理副作用逻辑。   

> 2，array(可选)：一个数组，用于控制执行。

```js
import { useState, useEffect } from 'react';

const Example = (props) =>{  

  const [count, setCount] = useState(0);

  useEffect(()=>{
      // 更新页面标题
      document.title = `你点击了${count}次`;
  },[])
  
  return (
    <div>
      <p>你点击了{count}次</p>
      <button onClick={() => setCount(count + 1)}>
        点击
      </button>
    </div>
  );
}
```  
<br/>   

### callback 副作用逻辑    
```js
useEffect(callback,array)
```
callback(回调函数)是`useEffect`的第一个参数，你所有的副作用逻辑都应该在这里处理。

另外你可以在callback中返回一个函数，用于清理工作。
```js
useEffect(()=>{
    // 副作用逻辑
    return ()=>{
        // 清理工作，类似于 componentWillUnmount
    }
})
```
<br/>

### array 控制执行   
```js
useEffect(callback,array)
```
array(数组)是`useEffect`的第二个参数，它可以用于控制`useEffect`是否执行。  

主要分以下两种情况： 

> 1，如果是空数组，则只会执行一次(初次render之后)，相当于`componentDidMount`。  

> 2，如果数组内存在值，那么`useEffect`会在该数组发生改变后执行。    

下面是基本案例：   

```js
useEffect(()=>{
    // 该effect仅在初次渲染之后执行一次，相当于`componentDidMount`
},[])   
```

```js
useEffect(()=>{
    // 该effect会在初次渲染之后执行一次，同时当数组内的count发生改变时也会执行
    // 相当于componentDidUpdate
},[count])
```
数组内的值可以是组件的state，或者是外部传递的props属性，亦或者是其他的值。   
<br/>

### useEffect 在什么时候执行？  

**useEffect** 会在每一次`render`之后执行。包括初始`render`和更新`render`。
<br/> <br/>  

### 可以执行多个 `useEffect`吗 ？ 

我们可以同时使用多个`useEffect`，如下：   
```js  
const App = () =>{    

    const [ user, setUser ] = useState(null);

    useEffect(()=>{
        // 初始化，获取数据，仅执行一次
        setUser(userData);
    },[])  

    useEffect(()=>{
        // 更新数据
    })  

    return (
        <div> 
            <p> { user && user.name } </p>
            <button onClick={()=> setUser() } >点击</button>
        </div>
    )
}
```

### useEffect 处理数据请求       
```js  
const App = () =>{    
    const [ user, setUser ] = useState(null);  

    const fetchUser = async () =>{
        const result = await fetch("./user.json").then(res=>res.json());
        setUser(result.user);
    }
    useEffect(()=>{
        fetchUser(); 
    },[])  
    return (
        <div> 
            <p> { user && user.name } </p>
            <button onClick={()=> setUser() } >点击</button>
        </div>
    )
}
```

### useEffect清理机制       

react中有两种常见的副作用，一种是需要清理的，一种是不需要清理的。  

> 1，网络请求、DOM修改和日志记录等，这些是不需要清理的。`useEffect`会自动处理。    

> 2，订阅和取消订阅，事件监听和取消事件监听，这种是需要清理的。  

下面是useEffect清理机制:

> 1，useEffect在每次执行之前都会自动清理之前的effect。   

> 2，effect中可以返回一个函数用于清理工作

