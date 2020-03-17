# 为什么需要css处理方案？  
css样式是前端开发中非常重要的一环，做开发时我们需要有一套完善的css处理方案来处理很多样式问题。
主要是因为我们在使用原生css做开发时，经常会遇到一些难题，比如说：  
> 1，css代码重用的问题  

> 2，class命名重复的问题   

> 3，不支持嵌套写法，很不方便  

> 4，没有压缩合并，css文件比较大  

> 5，不能使用变量，不够灵活  

> 6，一些未来的css语法不兼容  

....  

原生css的问题很多，上面只是一些举例。css社区为了解决这些难题，同时也为了提高我们写样式的效率和质量，推出了很多种css处理方案，比如前期的预处理器`sass/less`、再到模块化`css-module`、`postcss`，再到`css-in-js`。    

#### css处理方案有哪些？
css处理方案有很多种，可根据自己的需要来配置合适的css处理方案。  

下面我们来看看，具体有哪些css处理方案

##### 1，原生样式
内联样式:
```js
const App = (props) =>{
    
    return <div className="wrap" >
       <div style={{ color:"red", fontSize:14 }} > hello word </div>
    </div>
}
```
外部样式:
```js
const App = (props) =>{
    return <div className="wrap" >
       hello word
    </div>
}
```
```css
.wrap{
    width:100%;
    height:200px;
}
```

##### 2，预处理器sass/less
`sass/less`是一种预处理器，是处理css非常好的方式，它允许你使用变量、css嵌套、计算等强大功能，为写css提供了非常多的便利。
```css
$color : #333; 
$height: 200px;   

.wrap{
    width:100%;
    height:$height;
    h2{                   
        font-szie: 18px;
        color:$color;
    }
}
```
编译之后：
```css
.wrap{
    width:100%;
    height:200px;
}
.wrap h2{
    font-szie: 18px;
    color:#333;
}
```

##### 3，css-module
`css-module`是处理样式的一种css模块化方案，它能让你随意地命名class，不用担心它会重复或污染全局。  

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

##### 4，postcss
[postcss](https://github.com/postcss/postcss)是一款使用插件去转换CSS的工具集。例如[autoprefixer](https://github.com/postcss/autoprefixer)，[cssnext](https://github.com/MoOx/postcss-cssnext)以及[postcss-modules](https://github.com/css-modules/postcss-modules)。而上面列举出的这些特性，都是由对应的postcss插件去实现的。  

##### 5，css-in-js (推荐)
`css-in-js`是使用js编写css样式的一种处理方案。它有很多非常棒的实现，比如组件化style`styled-components`、[emotion](https://github.com/emotion-js/emotion)等等。

以[styled-components](https://github.com/styled-components/styled-components)为例，`styled-components`可以说是集大成者，也是开拓者。它集成了`css-module`和`autoprefixer`的精髓，也实现了超前的`组件化style`，让你如流水般写css。
```js
import styled from 'styled-components'

const Button = styled.button`  
  background: transparent;
  color: white;
  ${props => props.primary && css`
    background: white;
    color: palevioletred;
  `}
`
// 上面styled.button`` 相当于 styled.button()  

const App = (props) =>{
    return <div className="wrap" >
       <Button> 提交  </Button>
       <Button primary > 提交  </Button>
    </div>
}
```

