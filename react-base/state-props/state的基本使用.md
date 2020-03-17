# state的基本使用

### state是什么 ？

简单来讲，state就是react组件的状态。在组件内，state是一个object。

state分为本地状态和外部状态，本地状态也就是组件内部状态，它必须添加在组件`state对象`上。  

外部状态也就是从组件外部传进来的状态，外部状态通常是由第三方状态管理器进行管理。

> 注意：函数组件本身没有生命周期，也不能使用state，但借助`react hook`可以使用state和生命周期。

### state如何定义 ?  
定义state非常简单，只需要在class组件内添加`state`对象属性即可。state对象内的属性就是组件本地状态。 

通过`this.state`即可访问到组件本地状态。

比如下面的`loading`就是react组件的一个本地状态。
```js
class App extends React.Component {  

    state = {
        loading: false  // 设置默认值为false
    } 

    render(){
        return <div>
            { this.state.loading? <div> 加载中... </div> : null }
        </div>
    }
}
```    

### 数据也是一种state  

我们从后台请求的数据也是一种state，如果是本地状态，我们通常把它添加在组件`state对象`上，然后再输出到jsx。
```js
class App extends React.Component {  

    state = {
        user: null
    } 

    // 这个生命周期方法在组件渲染完成时执行
    async componentDidMount(){
        // 向后台请求用户数据
        const user = await fetch("/api/user").then(res=>res.json());
        this.setState({  // 更新用户数据到state对象
            user
        })
    }

    render(){ 

        // 外部状态loading
        const { loading } = this.props; 

        // 通过this.state访问状态user
        const { user } = this.state;
        return <div>
            { user && user.name }
        </div>
    }
}
```
