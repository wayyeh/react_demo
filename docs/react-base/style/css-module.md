# css-module
`css-module`是处理样式的一种css模块化方案，它支持哈希class，组合class、class继承等特性，非常有利于我们编写样式。  
### 如何在cra中使用css-module ？  
[cra(create-react-app)](https://facebook.github.io/create-react-app/docs/getting-started)默认支持`css-module`，开箱即用。   

> 1，样式文件以 `[name].module.css`或`[name].module.scss`的形式命名 

> 2，以变量的形式导入样式文件，比如 `import styles from './style.module.css'; `  
  
> 3，className以变量引用的方式添加，比如 `className={ styles.title }`  

### 一，哈希class (默认) 
你可以随意命名class，最终css-module会在局部作用域内给class添加哈希值，确保class唯一而不重复。  
```js
import styles from './style.module.css';  

const App = (props) =>{
    return <div className="wrap" >
       <h2 className={ styles.title } > hello word </h2>
    </div>
}
```
style.module.css:
```css
.title{
    font-size: 17px;
    color: #f66;
}
```
编译之后：
```html
<h2 class="style_title__s0dsl" > hello word </h2>
```

### 二，非哈希class ( global(.className) ) 
css-modules 允许使用`:global(.className)`的语法，声明一个全局规则。凡是这样声明的class，都不会被编译成哈希字符串。  

style.module.css：
```css  
/* 默认哈希用法 */  
.title{
   color:#f66;
}  
/* global用法 */
:global(.wrap){
  color: green;
  background: red;
}
    

/* 编译后 */
.style_title__s0dsl{
  color:#f66;
}
.wrap{
   color: green;
   background: red;
}
```
> 注意：使用global的方式添加样式时，className需要以字符串的形式来命名，而不是变量引用  

```js  
import styles from './style.module.css';  

const App = () =>(
   <div className="wrap">
      hello，word
      <h2 className={ styles.title } ></h2>
   </div>
)
```

### 三，class组合 `composition`   

在`css-module`中，一个选择器可以继承另一个选择器的规则，这称为"组合"（"[composition](https://github.com/css-modules/css-modules#composition)"）。

```css
.className {
  color: green;
  background: red;
}

.otherClassName {
  composes: className;
  color: yellow;
}
```

### 四，class模块继承  
选择器也可以继承其他CSS文件里面的规则。
```css
/* another.css */  

.className {
  background-color: blue;
}
```  
通过`composes` 和 `from`组合，继承其他css模块中的css规则。
```css 
/* style.css */
.title {
  composes: className from './another.css';
  color: red;
}

```

### 五，使用变量  
`css-module`支持使用变量，不过需要安装 PostCSS 和 [postcss-modules-values](https://github.com/css-modules/postcss-modules-values)。
```css
/* 定义变量 */
@value white: #fff;
@value blue: #0c77f8;

/* 使用变量 */
.title {
  color: white;
  background-color: blue;
}
```  

### 六，css-module和sass结合使用  

css-module和sass都非常好用，但他们都有不足的地方，比如css-module不支持css嵌套写法，sass不支持哈希class等等。  

因此，如果将`css-module`和`sass`结合来使用，将会互相弥补，非常强大。幸运的是，[cra(create-react-app)](https://facebook.github.io/create-react-app/docs/getting-started)支持这样做。    

下面是一个例子：
```js
import styles from './style.module.scss';  

const App = (props) =>{
    return <div className={ styles.wrap } >
       <h2> hello word </h2>
    </div>
}
```
style.module.scss:
```css
.wrap{
    font-size: 17px;
    color: #f66;
    h2{
       font-size: 28px;
    }
}
```
