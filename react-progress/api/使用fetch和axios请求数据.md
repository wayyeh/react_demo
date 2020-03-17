# fetch和axios
[fetch](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API)和[axios](https://github.com/axios/axios)都是非常优秀的用于请求数据的API，不同在于，fetch是原生的API，[axios](https://github.com/axios/axios)则是基于ajax封装的一个模块。

### 基本使用

##### 1，class组件    

在class组件内处理数据请求的话，通常需要在`componentDidMount`生命周期方法内处理。

下面是一个例子：
```js
import axios from 'axios';  

class UserPage extends React.Component {  
    
    // 1，声明初始state
    state = {
        user: null
    }

    // 2，请求并更新数据
    async componentDidMount(){  

        // 使用fetch
        const user = await fetch("/api/user").then(res=>res.json());  
        if(user){
            this.setState({ user });
        }

        // 使用axios
        const result = await axios("/api/user");  
        if(result && result.data){
            this.setState({ user: result.data });
        }
        
    }

    render(){
        // 3，渲染数据
        const { user } = this.state;
        return (
            <div>
                当前登录用户是：<b> { user && user.name } </b>
            </div>
        )
    }
}  
```

##### 2，函数组件    

函数组件中我们可以借助`react hook`的`useEffect`来实现生命周期，然后我们就可以使用`async/await`请求数据。

```js
import React,{ useState, useEffect } from 'react';  

export default () =>{     

    // 1，声明初始state
    const [ user, setUser ] = useState(null);
    
    // 2，请求并更新数据
    useEffect(async ()=>{

        // 使用fetch
        const result = await fetch("/api/user").then(res=>res.json());  
        if(result){
            setUser({ user: result });
        }

        // 使用axios
        const result = await axios("/api/user");  
        if(result && result.data){
            setUser({ user: result.data });
        }

    })
   
    // 3，渲染数据
    return (
        <div>
            当前登录用户是：<b> { user && user.name } </b>
        </div>
    )
}
```
