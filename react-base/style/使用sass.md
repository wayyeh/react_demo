# 使用sass

sass是一种css预处理器，是处理css非常好的方式，它允许你使用变量、css嵌套、计算等强大功能，为写css提供了非常多的便利。

[cra(create-react-app)](https://facebook.github.io/create-react-app/)是支持sass的，但需要你安装它。

### 安装sass  

安装sass非常简单，只需要安装`node-sass`即可在`cra`中使用它。
```js
yarn add node-sass
```
安装好之后你就可以创建scss文件编写样式了。比如:

```js
import './style.scss';

const App = () =>{
    return <div className="wrap" >
        sass我来啦
    </div>
}
```
```css  
/* style.scss */ 

 .wrap{
    width:100%;
    height:200px;
 }
```  

### 一，样式嵌套
scss允许你嵌套写样式。
```css
/* sass嵌套写法 */
 .wrap{
    width:100%;
     h2{
         color:#333;
         font-size:18px;
     }
 }

/* 编译后 */  
.wrap{
    width:100%;
}
.wrap h2{
    color:#333;
    font-size:18px;
}
```

### 二，群组嵌套
```css
/* Sass代码 */
.wrap {
    h1, h2, h3 {
      margin-bottom: 0.8em
    }
}  

/*编译后*/
.wrap h1, .wrap h2, .wrap h3 { 
    margin-bottom: 0.8em; 
}
```

### 三，css属性嵌套
```css
/* Sass代码 */
.wrap {
  width:100%;
  border: {
    style: solid;
    width: 1px;
    color: #ccc;
  }
}  

/* 编译后 */
.wrap {
  width:100%;
  border-style: solid;
  border-width: 1px;
  border-color: #ccc;
}
```

### 四，使用变量
```css  
 $defaultColor: #333;
 $defaultFontSize: 16px;  

 .wrap{
    width:100%;
     h2{
         color: $defaultColor;
     }
     .content{
         font-size:$defaultFontSize;
         .box{
            padding: 1em 2em;
         }
     }
 }
```

......  

更多用法请参考[sass官方文档](http://sass-lang.com/)