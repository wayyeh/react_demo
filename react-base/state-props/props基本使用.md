
### props是什么 ？

简单来讲，props是一个object，是组件外部传进来的属性的集合。

props也可以是任意类型。

### 如何传递props ？

传递props非常简单，只需要在组件调用时作为组件属性添加给组件即可。
```js
// 调用组件时传递props
<App loading={ false } />
```

### 如何访问props ？
函数组件和class组件访问props的方式不同。函数组件的props通过函数传参获取，class组件通过访问`this.props`来获取。  

##### class组件:
```js
class App extends React.Component {  
    render(){   

        // 通过this.props即可访问到外部传进来的属性 
        const { loading } = this.props; 
        return <div>
            { loading? <div> 加载中... </div> : null }
        </div>
    }
} 

// 调用组件
<App loading={ false } />
```

##### 函数组件:
```js
const App = (props) =>{  
    return <div>
        { props.loading? <div> 加载中... </div> : null }
    </div>
}

// 调用组件
<App loading={ false } />
```

### props.children  
`props.children`是组件的一个属性，`children`就是组件的子元素。

如果组件在调用时嵌套了子元素，那么我们需要在组件中获取并渲染它，子元素才会显示出来。

```js
// 渲染子元素
const App = (props) =>{
    return <div>
        { props.children }
    </div>
}

// 调用时嵌套子元素
<App>
  <div> hello，我是APP组件的子元素 </div>
</App>
```
