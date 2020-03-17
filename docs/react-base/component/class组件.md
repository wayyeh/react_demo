# class 类组件

类组件顾名思义是通过class类来创建的组件。    

react提供了一个抽象的基类，也就是`React.Component`，它内置了很多生命周期方法，以及其他的一些特性，以帮助你创建react组件。 

你只需要创建一个class类并且通过`extends`来继承`React.Component`这个基类即可创建一个类组件。  

##### 1，基本定义
```js 
import React from 'react'; 

// 类组件定义 
class App extends React.Component {  
    // ...做一些事情
    render(){
        return (<div>
            hello，这是一个类组件
        </div>)
    }
}
```
> 类组件内必须要有render方法，并返回jsx

##### 2，使用`PureComponent`    

与`Component`相比，`PureComponent`做了一些简单优化，性能更好。 

```js 
import React from 'react';

// 类组件定义 
class App extends React.PureComponent {  
    // ...做一些事情
    render(){
        return (<div>
            hello，这是一个类组件
        </div>)
    }
}
```
>注意：使用`PureComponent`可能会导致一些问题，比如`react-router`的`Link`失效等问题。搭配`immutable.js`使用可避免这些问题。


### 三，类组件的使用
##### 闭合写法
```js 
import React from 'react'; 

// 函数组件定义
<App />
```
##### 嵌套写法  
嵌套使用的组件，可以通过`props`下的childdren属性获取到嵌套的子元素。
```js 
import React from 'react'; 

// 嵌套子元素
<App>
   <div> 我是App组件的子元素 </div>
</App>
   
   


```
App组件
```js
// App组件
class App extends React.Component {  
    // ...做一些事情
    render(){

        return (<div>
            { this.props.children }  
        </div>)
    }
}
```

##### 嵌套函数调用
组件调用时可嵌套函数时，可通过`props`下的childdren获取这个函数，并调用这个函数来渲染子元素。

```js 
import React from 'react'; 

// 调用App组件，通过嵌套函数的方式
<App>
   {(args)=><div> 我是App嵌套的子元素，但我是一个函数 </div>}
</App>

```
App组件
```js
// App组件
class App extends React.PureComponent {  
    // ...做一些事情
    render(){

        return (<div>
            { this.props.children(args) }   // 调用时可传入一些参数
        </div>)
    }
}
```
> 注意：嵌套的函数必须返回jsx，因此嵌套的函数本质上是一个函数组件  