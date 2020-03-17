# css-in-js  
### 什么是css-in-js ？
`css-in-js`是一种使用js编写css样式的css处理方案。它的实现方案有很多，比如[styled-components](https://github.com/styled-components/styled-components)、[polished](https://polished.js.org/)、[glamorous](https://github.com/paypal/glamorous)(paypal开源的，不再维护)、[radium](https://github.com/FormidableLabs/radium)、[emotion](https://github.com/emotion-js/emotion)等等。

其中最成熟的便是[styled-components](https://github.com/styled-components/styled-components)和[emotion](https://github.com/emotion-js/emotion)。它们真正意义上实现了`组件化style`，可以说是专门为react打造的。

这里以`styled-components`为例，其他的`css-in-js`方案可自行查看文档。

### styled-components简介 
[styled-components](https://github.com/styled-components/styled-components)是css-in-js主流的实现方案，同时也是`组件化style`的主流实现方案。

下面是`styled-components`的一些特性：  
> 1，`唯一class类名`：和css-module异曲同工，生成唯一类名，避免重复和全局污染，也不需要你费脑筋思考该如何命名。  

> 2，`无冗余css代码`：它的样式和组件绑定，组件调用则样式起作用。意味着你不需要关心如何检测和删除那些未使用的css代码。

> 3，`动态样式`： 它可以很简单地调整和拓展组件的样式，而不需要建立很多个class类来维护组件的样式。  

> 4，`自动添加兼容前缀`：和Autoprefixer类似，会自动添加浏览器兼容前缀以支持旧版浏览器。  

> 5，`支持变量和继承`：你可以使用变量来设置不同的样式，使用这些不同样式时只需要给样式组件传递一个参数即可。


### 安装styled-components

使用[styled-components](https://github.com/styled-components/styled-components)非常简单，和其他多数js包一样，把它安装下来即可开箱即用。
```js
yarn add styled-components
```

### es6标签模板语法
比如下面有一个函数`tag()`
```js
// 标签模板写法
tag`123`;

// 等同于
tag(123);
```

### styled-components的基本使用

`styled-components`提供了一系列的html标签函数，比如button、h1、h2、ul、div、p等等，标签函数调用时会生成相应的标签组件，比如Button、Div等等，可赋给变量随意命名。

##### 1，普通用法

`styled-components`主要基于es6的`标签模板语法`调用标签函数。比如下面：
```js
import styled from 'styled-components';  

// 标签模板 - 函数名后接模板字符串``
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// 使用
<App>
    <Title> 我是标题组件，自带样式 </Title> 
</App>
```

##### 2，css嵌套写法

`styled-components`支持css嵌套写法，包括标签和class等。
```js
import styled from 'styled-components';  

// 标签模板 - 函数名后接模板字符串``
const Content = styled.div`
  padding: 12px;
  width:100%;
  height:200px;
  border: 2px solid green;
  > h2 {
     color: palevioletred;
  }
  > .content {
    text-align: center;
    color: #999;
  }
`;

// 使用
<App>
    <Content>
       <h2> 我是标题 </h2>
       <div className="content" > 我是内容 </div>
    </Content>
</App>
```

##### 3，传递props属性
```js
import styled, { css } from 'styled-components';  

const Button = styled.button`
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border-radius: 5px;
  color: palevioletred;
  border: 2px solid palevioletred; 

  /* 传参 */
  ${props => props.primary && css`
    border: 2px solid mediumseagreen;
    color: mediumseagreen;
  `}
`

const App = (props) =>{
    return <div className="wrap" >
       <Button> 提交  </Button>
       <Button primary > 提交  </Button>
    </div>
}
```

##### 4，拓展样式组件
```js
import styled from 'styled-components';    

const Button = styled.button`
  background: palevioletred;
  color: white;
`

const ExtendingButton = styled(Button)`
  font-size:18px;
  padding: 5px 25px;
`;

const App = (props) =>{
    return <div className="wrap" >
       <Button> 提交 </Button>
       <ExtendingButton> 提交  </ExtendingButton>
    </div>
}
```

##### 5，拓展组件样式
```js
import styled from 'styled-components';    

const Link = ({ className, children }) => (
  <a className={className}>
    {children}
  </a>
);

const StyledLink = styled(Link)`
  color: palevioletred;
  font-weight: bold;
`;

const App = (props) =>{
    return <div className="wrap" >
       <Link>跳转</Link>
       <StyledLink>跳转</StyledLink>
    </div>
}
```

.... 

更多用法请查看[styled-components文档](https://www.styled-components.com/docs)