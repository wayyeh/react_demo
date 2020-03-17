## Refs是什么 ？

`Refs(转发)`是react提供的一种访问DOM节点的方法。

> 官方提醒：不要过度使用`Refs`，并且尽量少地操作DOM

## 如何创建和使用Refs ?

创建refs有两种方式，分别是:

> 1，`React.createRef()`   

> 2，`回调式refs`  

#### 1，React.createRef()
使用`React.createRef()`方法就可以创建refs。
```js
class MyComponent extends React.Component {    

  // 1，创建ref
  myRef = React.createRef();  

  componentDidMount(){  

    // 3，通过ref访问DOM节点
    console.log(this.myRef); // 访问ref对象 { current: node }
    console.log(this.myRef.current); // 访问实际DOM节点
    console.log(this.myRef.current.innerHTML); // 访问DOM的html内容
  }

  render() { 
    // 2，挂载ref
    return <div ref={ this.myRef } > 内容 </div> ;  
  }
}
```

#### 2，回调refs  

除了使用`React.createRef()`方法来创建refs以外，你还可以通过回调函数来使用ref。
```js
class MyComponent extends React.Component {     

  // 1，创建类属性
  myRef = null;  

  componentDidMount(){  

    // 3，通过ref访问DOM节点
    console.log(this.myRef); // 直接获取到DOM节点
    console.log(this.myRef.innerHTML); // 访问DOM的html内容
  }
  
  render() { 
    // 2，通过ref回调函数来获取DOM节点
    return <div ref={ node=> this.myRef = node } > 内容 </div> ;  
  }
}
```
<!-- 
### 如何使用Refs ?     

#### 一，React.createRef()
使用`React.createRef()`方法就可以创建refs。
```js
class MyComponent extends React.Component {    
  // 1，创建ref
  myRef = React.createRef();  

  render() { 
    // 2，挂载ref
    return <div ref={ this.myRef } > 内容 </div> ;  
  }
}
```


##### 1，在class组件内部使用    
```js
class MyComponent extends React.Component {    
  // 1，创建ref
  myRef = React.createRef();  

  componentDidMount(){
    // 3，通过ref访问DOM节点
    console.log(this.myRef); // 访问ref对象 { current: node }
    console.log(this.myRef.current); // 访问实际DOM节点
    console.log(this.myRef.current.innerHTML); // 访问DOM的html内容
    console.log(this.myRef.current.innerText); // 访问DOM的文本内容
  }

  render() { 
    // 2，挂载ref
    return <div ref={ this.myRef } > 内容 </div> ;  
  }
}
```

##### 2，在class组件上使用      
refs不仅能在DOM上面用，也能在组件上使用(仅限class组件)，通常用于父子组件的DOM交互(尽量少地使用)。
   
下面是一个例子：  
```js
// 父组件
class Parent extends React.Component {  

  childElement = null;  // 1，父组件内定义类属性

  render() {
    // 2，给子组件传递 ref回调函数 ，可获取到子组件的DOM，并赋给 childElement 类属性
    return (
      <Child inputRef={el => this.inputElement = el} />
    );
  }
}     

// 3，子组件内获取父组件ref回调函数，并挂载给DOM节点
function Child(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}
```  

##### 3，在函数组件内部使用    
```js
const App = () =>{

    let textInput = React.createRef(); // 1，创建ref

    const getInputValue=()=>{
        console.log(textInput.current);  // 3，访问DOM
        console.log(textInput.current.value);
    }
    
    // 2，挂载ref
    return (
        <div>
            <input
              type="text"
              ref={textInput}
            />
            <button onClick={ this.getInputValue } > 获取input值 </button>
        </div>
    )
}
```

##### 2，在函数组件中使用    

#### 二，回调refs
除了使用`React.createRef()`方法来创建refs以外，还可以使用回调函数来创建ref。
```js
class MyComponent extends React.Component {      
  // 创建类属性
  myRef = null;  

  componentDidMount(){
    // 
  }
  
  render() { 
    return <div ref={ refs=> this.myRef = refs } > 内容 </div> ;  
  }
}
```

### 如何使用Refs ?

Refs的使用分为几种不同的情况:  

- `class组件的DOM添加Refs`   

- `给class组件添加Refs`   

- `给函数组件的DOM添加Refs`

> 注意：不能给函数组件添加refs，因为它没有实例

### 一，回调式Refs     
通过回调函数获取DOM的ref，并赋给类属性，从而实现对DOM的访问。
```js
class MyComponent extends React.Component {   

  divRef = null;  // 1，先声明一个类属性

  componentDidMount(){ 

      // 3，访问DOM  

      console.log(this.divRef); // DOM节点
      console.log(this.divRef.innerHTML); // DOM节点的内容
  }

  render() { 

    // 2，通过回调函数获取ref，并赋给 divRef   

    return <div ref={ element=> this.divRef = element } > 内容 </div> ;  
  }
}
```

### 二，class组件的DOM添加Refs  
在class组件内使用Refs非常简单，只需要通过`React.createRef()`方法创建一个`ref`，然后挂载到DOM节点就可以通过ref访问DOM了。   

```js
class MyComponent extends React.Component { 

  myRef = React.createRef();  // 1，创建ref

  componentDidMount(){  

      // 3，访问ref对象
      console.log(this.myRef); 
      console.log(this.myRef.current); // 访问实际DOM节点
      console.log(this.myRef.current.innerHTML); // 访问DOM的html内容
      console.log(this.myRef.current.innerText); // 访问DOM的文本内容
  }

  render() {
    return <div ref={ this.myRef } > 内容 </div> ;  // 2，挂载ref
  }
}
```

### 三，给class组件添加Refs  
refs不仅能在DOM上面用，也能在组件上使用(仅限class组件)，通常用于父子组件的DOM交互(尽量少地使用)。
   
下面是一个例子：  
```js
// 父组件
class Parent extends React.Component {  

  childElement = null;  // 1，父组件内定义类属性

  render() {
    // 2，给子组件传递 ref回调函数 ，可获取到子组件的DOM，并赋给 childElement 类属性
    return (
      <Child inputRef={el => this.inputElement = el} />
    );
  }
}     

// 3，子组件内获取父组件ref回调函数，并挂载给DOM节点
function Child(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}
```


### 四，给函数组件的DOM添加Refs
```js
const App = () =>{

    let textInput = React.createRef(); // 1，创建ref

    const getInputValue=()=>{
        console.log(textInput.current);  // 3，访问DOM
        console.log(textInput.current.value);
    }
    
    // 2，挂载ref
    return (
        <div>
            <input
              type="text"
              ref={textInput}
            />
            <button onClick={ this.getInputValue } > 获取input值 </button>
        </div>
    )
}
```

> 注意：不能给函数组件添加refs，因为它没有实例    

```js  

const MyFunctionalComponent =()=>{
  return <input />;
}

class Parent extends React.Component {  

  textInput = React.createRef();  

  render() {
    // 错误的做法 ❌
    return (
      <MyFunctionalComponent ref={this.textInput} />
    );
  }
}
``` -->