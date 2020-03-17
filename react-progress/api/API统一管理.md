# API统一管理
一个成熟的应用程序，通常需要统一管理API，这样有利于我们协作开发和维护。  

### 封装请求方法   

首先，我们需要封装一个统一的请求方法。  

不管是`fetch`还是`axios`，它们请求的配置方式都是差不多的，因此我们可以对它们进行一些封装以达到代码复用。

##### 1，封装`fetch`请求方法  
```js
// request.js
export default ({ url, method, headers, data },options={})=>{
    return fetch(url,{
        // *GET, POST, PUT, DELETE。
        method: method||'GET', 
        // 发送给后台的数据
        body: data ? JSON.stringify(data) : null, 
        // 请求头
        headers: headers || {
            'content-type': 'application/json'
        },
        mode: 'cors', // 跨域处理
        ...options    // 其他配置项
    }).then(res=>res.json());
}
```
使用案例：  
```js
import request from './utils/request';  

const result = request({ url: "/api/user", data: { id: "userId" } });
```

##### 2，封装`axios`请求方法  
```js
// request.js
export default ({ url, method, headers, data },options={})=>{
    return axios(url,{
        // *GET, POST, PUT, DELETE。
        method: method||'GET', 
        // 发送给后台的数据
        data, 
        // 请求头
        headers: headers || {
            'content-type': 'application/json'
        },
        ...options    // 其他配置项
    })
}
```
使用案例：  
```js
import request from './utils/request';  

const result = request({ url: "/api/user", data: { id: "userId" } });
```


### 集中管理请求API  

如果我们将各个请求分散在每个组件中定义，这样是非常麻烦和难以维护的。因此比较好的做法是将它们集中起来管理，方便开发和维护。  

通常我们可以按功能模块来管理。比如用户模块的请求函数，单独写在一个`user.js`模块里面。

下面是一个案例：  

```js
// 用户请求模块
// services/user.js
import request from '../utils/request';  

export default class user {   

    // 获取所有用户
    static gets(){
        return request({
            url: "/api/user"
        })
    }  

    // 获取指定用户
    static get(id){
        return request({
            url: `/api/user/${ id }`
        })
    }   

    // 新增用户
    static create(data){
        return request({
            url: "/api/user",
            method: 'POST',
            data
        })
    }   

    // 更新用户信息
    static put(id,data){
        return request({
            url: `/api/user/${ id }`,
            method: 'PUT',
            data
        })
    }   

    // 删除用户
    static delete(id){
        return request({
            url: `/api/user/${ id }`,
            method: 'DELETE'
        })
    }
}
```

基本使用：  
```js  
import userapi from '../services/user';  

class UserPage extends React.Component {

    state = {
        user: null
    }

    async componentDidMount(){
        // 调用请求函数
        const user  = await userapi.get("userid");
        if(user){
            this.setState({ user });
        }
    }   

    render(){
        const { user } = this.state;
        return (
            <div>
                当前用户是：<div> { user && user.name } </div>
            </div>
        )
    }
}
```
