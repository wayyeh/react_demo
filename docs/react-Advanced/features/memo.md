# React.memo  

React.memo 是一个高阶组件。它的主要作用在于性能优化，和React.PureComponent 类似，不同的是React.memo包裹函数式组件，而不是类组件。

如果传入的props没有变化，则会跳过渲染，使用上一次渲染结果。

下面是一个案例： 
```js
const MyComponent = React.memo((props)=>{
    return (
        <div>
            被优化的函数组件
        </div>
    )
});
```

#### 自定义比较函数
```js
const MyComponent = (props) =>{
    return (
        <div>
            { props.name }
        </div>
    )
}  

// 比较函数
const areEqual = (prevProps, nextProps) =>{

   if(prevProps.name !== nextProps.name){
       // 和类组件的shouldComponentUpdate() 方法不同，如果不相等则返回false
       return false;
   }
}
export default React.memo(MyComponent, areEqual);

```

