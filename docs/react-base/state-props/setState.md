### setState是什么方法 ？  

`setState(stateObject,callback)`方法是class组件自带的方法，它主要用于更新组件的状态(state)。  

setState方法是异步执行的，它接收两个参数。  

> stateObject：第一个参数，是一个object或函数，里面是你最新的state,如果是函数则必须返回一个object。  

> callback：state更新后执行的回调函数。

!> 注意：你不能在render方法中直接调用`setState`方法，否则会报错。

### 如何访问setState ？

很简单，在class组件内通过`this`来访问即可。`this.setState`

### setState基本使用    
setState用于更新组件状态，使用它非常简单。 
```js
class App extends React.Component {  

    state = {
        count: 0
    } 

    addCount(){
        const { count } = this.state;
        this.setState({
            count: count+1
        })
    }

    render(){ 
        const { count } = this.state;
        return <div>
           <div> { count } </div> 
           <button onClick={ this.addCount.bind(this) }  > 增加 </button>
        </div>
    }
}
```
### state双向绑定  
react也可以实现双向绑定，使用`setState`方法即可。下面是一个例子：
```js
class App extends React.Component {  

    state = {
        value: null
    }  

    render(){ 
        return <div>
            <input 
              type="text" 
              value={ this.state.value }
              onChange={e=>this.setState({ value: e.target.value })} 
            />  
            <p> 输入的值是: { this.state.value } </p>
        </div>
    }
}
```

### state同步更新     

在react开发中经常会有这种需求，要先后更新多个state，后一个更新必须在前一个state更新完毕后执行。也就是串行执行setState。比如下面这个案例：  
```js
class App extends React.Component {  

    state = {
        user: null,
        posts: null
    }  

    componentDidMount(){
        // 由于是异步，下面两个setState是同时执行的
        setState({ user: {} });
        setState({ posts: [] });
    }

    render(){ 
        return <div>
            hello word
        </div>
    }
}
```

但是`setState`方法是异步的，也就是当有多个`setState`时他们是同时执行的，并不能实现执行完一个setState后，再执行下一个setState。

当我们要实现这种需求的时候，我们只能借助setState方法的第二个参数来实现，也就是callback。下面是一个例子：
```js
class App extends React.Component {  

    state = {
        user: null,
        posts: null
    }  

    componentDidMount(){
        // 通过回调函数来实现串行更新state
        setState({ 
            value: { name:"ben" }
        },()=>{
            setState({ posts: [] });
        });
    }

    render(){ 
        return <div>
            hello word
        </div>
    }
}
```

但是我们还有更简洁的方式，就是借助`async/await`语法。下面是一个例子：

```js
class App extends React.Component {  

    state = {
        user: null,
        posts: null
    }  

    async componentDidMount(){
        await setState({ user: { name:"ben" } });
        await setState({ posts: [] });
    }

    render(){ 
        return <div>
            hello word
        </div>
    }
}
```

### 封装同步setState
我们还可以使用`promise`和`async/await`封装一个同步setState方法，方便我们使用。下面是一个例子： 

```js
class App extends React.Component {  

    state = {
        user: null,
        posts: null
    }  

    setStateAsync(stateObject){
        return new Promise((resolve) => {
            this.setState(stateObject, resolve);
        });
    }

    async componentDidMount(){
        await this.setStateAsync({ value: 1 });
        await this.setStateAsync({ posts: [] });
    }

    render(){ 
        return <div>
            hello word
        </div>
    }
}
```