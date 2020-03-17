# useContext - 上下文   

[useContext](https://reactjs.org/docs/hooks-reference.html#usecontext)是为了方便我们使用[context](https://reactjs.org/docs/context.html)而提出的一个API。

### context 

通常我们可以使用第三方状态管理器来实现全局数据共享，管理状态，比如redux、dva、mobx。

而context(上下文)是react提供的一个用于实现数据共享的API。它可以解决需要通过多层嵌套传递props的问题。  

主要通过以下三步：  
> 1，通过React.createContext()创建Context对象    

> 2，使用Context.Provider包裹组件，给它的后代组件提供数据   

> 3，Context.Provider所有的后代组件，都可以通过Context.Consumer获取Context数据

下面是context的一个使用案例：   

1，创建Context
```js
const Context = React.createContext();
```    

2，使用Context.Provider包裹组件  

```js
<Context.Provider value = { store } >
    <MyComponent />
</Context.Provider>
```  

3，使用Context.Consumer获取共享的数据

```js
// MyComponent组件  
<Context.Consumer>
   {value =>{
       // value就是通过context共享的数据，这里是store
       // ...
   }}
</Context.Consumer>
```  

### useContext(context)  

`useContext(context)`是针对`context`(上下文)提出的一个API，它接受`React.createContext()`的返回值作为参数，也就是context对象，并返回最近的context。

使用useContext将不再需要Provider和Consumer。

当最近的`context`更新时，那么使用该context的hook将会重新渲染。

### 基本使用  
```js
const Context = React.createContext({ loading: false , name: "jack" });

// 组件1
const OnePage = () =>{

    const ctx = useContext(Context);

    return (
        <div>
            { ctx.loading && "Loading..." }
        </div>
    )
}


// 组件2
const TwoPage = () =>{

    const ctx = useContext(Context);

    return (
        <div>
            { ctx.name && ctx.name }
        </div>
    )
}
```
