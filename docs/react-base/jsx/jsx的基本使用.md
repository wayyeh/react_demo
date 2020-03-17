# jsx的基本使用   
jsx是js的拓展语法，因此它能和js很好地结合使用。
### 如何编写html标签 ？ 
在jsx中直接编写即可。
```js
// 使用html标签
const App = () =>{
    return <div>
        这里是jsx
    </div>
}
```
### 如何编写样式 ？ 
##### 1，内联样式
内联样式需要使用`style`属性，它的值必须是一个object，样式可写在这个object中。可使用js计算。
```js
const App = () =>{
    return <div style={{ color:"red",fontSize:15, width: document.body.clientWidth }} >
        这里是jsx
    </div>
}
```
##### 2，外部样式
外部样式需要加载css文件，然后使用`className`定义类名。
```js
import './style.css';  

const App = () =>{
    return <div className="wrap" >
        这里是jsx
    </div>
}
```
style.css
```css
.wrap{
    width:100%;
    height:100%;
    font-size:16px;
}
 
```
### 如何使用javascript表达式 ？ 
jsx中可使用花括号`{}`来输入js表达式。

##### 1，普通使用
```js
// UserPage组件
const UserPage = (props) =>{
    const { name } = props;
    return <div className="wrap" >
        <p> 我的名字是: { name } </p>
    </div>
}

```
##### 2，jsx用作表达式  
jsx也可以作为一种表达式使用，把它赋给变量。  

```js
// UserPage组件
const UserPage = (props) =>{

    const title = <h1> 这里是个人主页 </h1>;  

    return <div className="wrap" >
        { title }
        <p> 我的名字是: { name } </p>
    </div>
}
```

##### 3，传递属性  
传递属性时，如果是变量、数字或布尔值，也需要使用花括号`{}`来传递。
```js
// UserPage组件
const UserPage = (props) =>{

    const title = <h1> 这里是个人主页 </h1>;  

    return <div className="wrap" >

        { title }
        <p> 我的名字是: { name } </p>

        <UserProfile
            name = { name }
            age = { 23 }
            gender = "男"
            loading = { false }
        />
    </div>
}
```

##### 4，输出html  
输出html需要使用`dangerouslySetInnerHTML`属性。这个属性相当于`innerHTML`。
```js
const App = (props) =>{

    const content = "<p> 我是html字符串 </p>";  

    return <div className="wrap" >
       <div dangerouslySetInnerHTML={{ __html: content }} ></div>
    </div>
}
```

##### 5，输出事件 
```js
const App = (props) =>{

    const onSubmit = () =>{
        console.log("提交数据~");
    }

    return <div className="wrap" >
       <button onClick={ onSubmit } >提交</button>
    </div>
}
```

### 如何加载图片 ？
###### 使用require加载
```js
const App = (props) =>{
    return <div className="wrap" >
       <img src={ require("./test.png") } />
    </div>
}
```
###### 使用import加载
```js
import Img from './test.png';  

const App = (props) =>{
    return <div className="wrap" >
       <img src={ Img } />
    </div>
}
```

### 如何使用注释 ？
在jsx中使用注释，要使用`{/* 注释的内容 */}`
```js
const App = (props) =>{
    return <div className="wrap" >
       {/* <p>hello word</p> */}
    </div>
}
```