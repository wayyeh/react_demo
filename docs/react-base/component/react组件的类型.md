# react组件的类型

按写法分，react组件主要分为三种，分别是`传统组件( createClass )`、`类组件(class component)`、`函数组件(function component)`。

如果按功能分，又可以分为很多种，比如`顶层组件`、`布局组件`、`容器组件( container component )`、`展示组件(show component)`等等。
  
## 按写法划分
### 一，传统组件  createClass

传统组件是react最初创建组件的方式，它主要通过调用`React.createClass`方法来创建组件。它需要你传入组件的相关配置信息，比如`render`方法等等。

但目前传统组件已经被淘汰，`react v16`以后不再支持。
下面是一个传统组件:
```js
// 传统组件
var App = React.createClass({
    render:function(){
        return (
          <div>hello，这是一个类组件</div>
        );
    },
});
ReactDOM.render(
        <App />,
        document.getElementById('content')
);
```

### 二，class类组件  Class Component  
类组件顾名思义是通过class类来创建的组件。它依赖于class语法。下面是一个class组件:
```js 
// 类组件定义  
// React.Component是react提供的用于创建类组件的基类
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


### 三，函数组件 - Fuction Component  
函数组件非常简单，一个函数内返回jsx，这个函数就是一个函数组件。  
> 函数组件本身没有生命周期，但react hook出来以后，函数组件也能使用生命周期。  

```js 
// 函数组件定义
const App =(props)=>{  

    // ...做一些事情
    return (<div>
        hello，这是一个类组件
    </div>)
}
```

## 按功能划分  
##### 顶层组件 和 布局组件
```js
  // <App>为顶层组件，Header、Content、Footer为布局组件
  <App>
    <Header />
    <Content />
    <Footer />
  </App>
```  

##### 容器组件 和 容器子组件
容器组件就是一个模块级别的包装组件，非容器组件就是容器组件的子组件
```js
  //  用户主页模块，UserPage是容器组件，UserProfile和UserWork则是容器组件的子组件
  <UserPage>
    <UserProfile />
    <UserWork />
  </UserPage>
```

##### 展示组件  
纯展示组件，没有交互性。
```js
  //  展示组件
  <UserProfile>
    <ProfileCard />
  </UserProfile>
```
