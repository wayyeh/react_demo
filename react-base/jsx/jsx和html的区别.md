### 一，什么是jsx ？

jsx是一种独立的js标签语法，它既不是字符串也不是HTML。  

但jsx是在html基础上使用js开发出来的，因此它具有几乎所有的html特性。你完全可以把它当html来使用。
```js
// jsx
const element = <h1>Hello, world!</h1>;
```

从本质上讲，jsx 只是为 `React.createElement(component, props, ...children)` 函数提供的语法糖。

> React.createElement方法主要用于生成 `React elements`，这是一种`虚拟DOM`。

### 二，jsx和html的区别  

> 1，jsx和html是两种不同的标签语法，但jsx拥有和html几乎相同的写法和特性(标签、标签属性、事件名等等)    

> 2，jsx是js语法拓展，而html则是原生的标签语法    

> 3，jsx可以使用js表达式，html不能   

> 4，jsx天然预防xss漏洞，html不能   

> 5，jsx事件和标签属性使用驼峰命名，html不需要   

> 6，jsx会被转换成`React Dom`，然后再转换为`原生DOM`，而html则直接生成`原生dom`  

> 7，jsx和html的部分属性有差异，比如html的`class`对应jsx的`className`  

##### 总的来说，jsx可以说是javascript版的html。  

### 三，jsx和html的属性差异

#### 1，命名方式  
在jsx中，所有的html属性和事件名都需要使用驼峰命名，有两种例外，那就是`aria-*`和`data-*`。

###### 属性名  

```js
// `minLength`使用的是驼峰命名，而html中则是`minlength`
 <App>
    <input type="text" minLength="10"  />
 </App>
```
###### 事件名  

```js
//  react中onChange、onClick使用的是驼峰命名，而在html中则是onchange、onclick
<App>
    <input type="text" onChange={ (e)=>console.log(e.target.value) }  />
    <button onClick={ ()=>alert("点击提交") }>提交</button>
 </App>
```

###### 样式名 (内联样式) 
jsx中使用内联样式时，也需要驼峰命名，且样式需要写在一个object中，并赋给style属性。  

jsx内联样式:
```js  
// jsx驼峰内联样式
<App>
    <input type="text" style={{ backgroundColor:"#f66", fontSize: 15 }}  />
</App> 
```
原生html内联样式:
```js  
// 原生内联样式
<input type="text" style="background-color:red;font-size:15px;"  />
```

#### 2，属性差异

##### 1，className 
html中的css类名为`class`，而jsx中css类名则是`className`
```js  
<App>
    <input type="text" className="myclass" />
</App> 
```

##### 2，value 和 defaultValue 
在jsx中除了可以用`value`属性设置`<input>` 和 `<textarea>`的值以外，还可以使用`defaultValue`属性设置首次装载时的值。
```js  
<App>
    <input type="text" value="我是固定值" />
    <input type="text" defaultValue="我是初始默认值" />
</App> 
```

##### 3，checked 和 defaultChecked

`checked`可用于设置`checkbox` 和 `radio`是否选中，defaultChecked可用于设置默认选中的项(首次载入组件时是否选中)。
```js  
<App>
    <input type="radio" checked="checked" />白色
    <input type="radio" defaultChecked={true} />红色
</App> 
```

##### 4，innerHTML 和 dangerouslySetInnerHTML
`dangerouslySetInnerHTML`相当于html的`innerHTML`。它接受一个对象作为值，并且对象中使用`__html`来指定html字符串。
```js  
// html字符串
const htmlstr = `<p>hello word</p>`;

// jsx
<App>
    <div dangerouslySetInnerHTML={{ __html: htmlstr }} >
    </div>
</App> 
```