# 事件处理

react有自己的事件系统，和原生的事件处理程序有些许不同。

### 一，react中使用事件

react事件和原生事件的几点区别：
> 1，事件名不同，react事件名必须使用驼峰命名   
  
> 2，原生事件处理程序为字符串调用，而react则是一个函数

原生的方式：  
```js
// 原生事件处理，事件名小写，事件处理程序使用字符串
<button onclick="submit()">
  提交
</button>
```
react的方式：
```js
// react事件处理，事件名必须使用驼峰命名，事件处理程序使用变量或函数
<button onClick={ submit }>
  提交
</button>
```

### 二，事件绑定(bind)

react规定，在class组件内使用事件时需要使用`bind`来绑定`this`，否则的话`this`会是`undefined`。

```js
class App extends React.Component {
    
    onSubmit(){
        // 通过bind绑定this之后，才可以访问this，否则会是undefined
        console.log(this); 
    }

    render(){
        // 使用bind绑定this
        return (
            <button onClick = { this.onSubmit.bind(this) } ></button>
        )
    }
}
```

上面的效果等同于下面：  

```js
class App extends React.Component {
    
    onSubmit(){
        // 可以访问this
        console.log(this); 
    }

    render(){
        // 不使用bind绑定this
        return (
            <button onClick = {e=>this.onSubmit(e)} > 提交 </button>
        )
    }
}
```


### 三，事件传参

react事件传参需要先使用`bind`绑定`this`，然后再传递参数。

##### 1，函数组件事件传参：
```js  

const App = () =>{
    const onSubmit = (arg1,arg1,e) =>{
        console.log(arg1);  // 1
        console.log(arg2);  // 2
        console.log(e);     // event对象
    } 
    return (
      <div>
         <button onClick={ onSubmit.bind(this,1,2) } > 提交 </button>
      </div>
    )
}
```

##### 2，class组件事件传参：  
```js  
class App extends React.Component {
    
    onSubmit(arg1,arg2,e){
        console.log(arg1);  // 1
        console.log(arg2);  // 2
        console.log(e);     // event对象
    }

    render(){
        return (
            <button onClick = { this.onSubmit.bind(this,1,2) } > 提交 </button>
        )
    }
}
```


### 四，阻止事件默认行为  

react不支持通过`return false`阻止事件默认行为，要阻止事件默认行为必须使用`调用 preventDefault`。

原生阻止事件默认行为：
```js
<a href="https://www.baidu.com" onclick="console.log('阻止跳转.'); return false">
  跳转
</a>
```

react阻止事件默认行为： 
```js
const App = () =>{
    const onSubmit = (e) =>{
      console.log(e);
      e.preventDefault();
    }
    return (
      <div>
         <a href="https://www.baidu.com" onClick={ onSubmit } >跳转</a>
      </div>
    )
}
```