# flex弹性布局  

flex弹性布局是目前主流的页面布局方案，因此在react开发中也是必备的。

目前主流浏览器都已经支持flex，并且[cra(create-react-app)](https://facebook.github.io/create-react-app/docs/getting-started)内置了`Autoprefixer`插件，它会自动添加兼容性前缀，因此你必担心flex的兼容性问题。

#### flex基本使用
在react中使用flex弹性布局很简单，直接在样式中写flex语法即可。

比如，下面用flex来实现一个常见的`纵向三栏布局`： 

先看参考效果:   

![布局效果](../../images/shengbei.png)
  
下面是实现的代码：

组件页面布局
```js
import React from 'react';
import './App.css'; 

const App = () =>{
    return <div className="App">
        <header className="header" >这里是头部</header>
        <section className="content" >
            这里是内容区
        </section>
        <footer className="footer" >这里是固定尾部</footer>
    </div>
}
```
App.css
```css
.App{
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}  

.App .content{
   flex: 1;
}
```



