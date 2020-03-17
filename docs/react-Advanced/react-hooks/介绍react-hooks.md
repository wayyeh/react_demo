# 介绍Hooks

[React Hooks](https://reactjs.org/docs/hooks-intro.html)是React 16.8中新增的功能。它允许你在函数组件里使用state和其他React功能。

### React Hooks 解决了什么问题 ？  

#### 1，函数组件不能使用state   

在[React Hooks](https://reactjs.org/docs/hooks-intro.html)推出之前，函数组件通常只能用于一些简单而无交互的场景，比如信息展示。当需要交互的时候我们就得用臃肿的class组件来实现。  

在[React Hooks](https://reactjs.org/docs/hooks-intro.html)推出之后，函数组件能够使用state功能，并且比class组件更加简洁，更加好用。

可以预见的是，未来函数组件将会被大幅度地采用，这不仅能给我们带来非常爽的开发体验，同时也提高了我们的开发效率和质量。

<br/>   

#### 2，副作用的问题
通常数据获取、订阅、或手动修改`React DOM`这些行为，我们可以称之为`副作用(side effect)`。

[React Hooks](https://reactjs.org/docs/hooks-intro.html)提供了`useEffect`这个API来处理组件的副作用问题。

那也就意味着你可以在函数组件内进行数据获取、订阅等操作。

而在class组件里我们需要依赖`componentDidMount`，`componentDidUpdate`，和 `componentWillUnmount`这几个生命周期方法来实现。

`useEffect`可以说是对这几个生命周期方法的统一。  
<br/>   

#### 3，有状态的逻辑重用的问题

在开发中我们经常会遇到一些组件复用的问题，比如公共`<Button>`、弹窗、布局、卡片等等，又或者说一些可复用的业务逻辑，比如数据请求、关注和取消关注等等。

[React Hooks](https://reactjs.org/docs/hooks-intro.html)可以很轻松地实现这些逻辑的封装，从而达到组件复用的效果。你完全可以根据你的需要创建自定义的hooks。

简单点说就是，React Hooks解决了代码复用的问题。

这里有一个[Hooks指南网站](https://www.hooks.guide)，它里面封装了几十个非常好用的`hooks`，并且还在不断地新增。

<br/>   

#### 4，复杂状态管理的问题  

对于复杂的状态管理，过去我们使用`redux`、`dva`、`mobx`等第三方状态管理器来管理。  

[React Hooks](https://reactjs.org/docs/hooks-intro.html)推出之后，我们可以不再依赖这些第三方状态管理器了，我们只需要依据React Hooks提供的API就可以实现复杂的状态管理。  

主要就是`useReducer`、`useContext`这些API。

<br/>   

#### 5，效率和质量的问题  

[React Hooks](https://reactjs.org/docs/hooks-intro.html)是纯函数式开发，相比于臃肿的class组件，函数组件开发体验更好，开发效率更高，应用性能更好。  

[React Hooks](https://reactjs.org/docs/hooks-intro.html)扩大了函数组件的应用范围，意味着我们可以在绝大都数应用场景使用函数组件进行快速开发。

