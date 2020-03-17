# es-module 模块化   

以前javascript是没有模块体系的，后来js社区提出了三种模块化方案，主要是`CommonJS`，`AMD`，`CMD`三大规范。比如nodejs的模块系统`require`、webpack等都是以`CommonJS`规范来实现的；requirejs是基于`AMD`规范来实现的，seajs是基于`CMD`规范实现的。

但这些都不是最好的方式，于是es6提出了官方的`es-module`模块化方案，成为浏览器和服务器通用的模块解决方案。  

es-module主要由两个命令构成：export和import，即导出和导入。   

使用es-module时，可以说一个js文件就是一个模块，文件内的变量、函数、类需要export，然后才能在另一个模块中使用import来引用。
## 一，基本使用

##### 普通导入导出
```js
// test1.js 
// 导出 - export一个count变量
export const count = 100;

// test2.js 
// 导入 - import text1.js 的count
import { count } from './test1';
```


##### 默认导入导出
```js
// test1.js 
// 默认导出一个count变量
const count = 100;
export default count;  // 使用默认导出时，不能使用变量声明表达式
  
  
// 导入时是默认的变量名`default`，你可以定义一个新的名字，或使用`default as`重命名  

// test2.js 
import count from './test1';
或
import anyname from './test1'; // anyname可以是任意变量名  

// 等同于  
import { default as count }  from './test1';
或
import { default as anyname }  from './test1';
```
> 使用默认导出，在其导入时其变量名可自定义


##### 多种导入导出
```js
// test1.js 
export const Component = {};
export default = {};


// test2.js 
import React,{ Component } from './test1';  // React是默认导出的{}，默认导出的变量是可以自定义的

```


##### 复合写法
```js
export { foo, bar } from 'my_module';

// 等同于
import { foo, bar } from 'my_module';
export { foo, bar };

```

#### 使用`* as` 整体导入
首先，在`validate.js`定义两个验证函数
```js
// validate.js

// 验证手机号
export function checkphone(phone) {
  ...
  return phone;
}
// 验证email
export function checkemail(email) {
  ...
  return email;
}

```

正常导入
```js
// test.js
import { checkphone,checkemail } from './validate';
console.log(checkphone);
console.log(checkemail);
```

使用`* as` 整体导入
```js
// test.js
import * as validates from './validate';
console.log(validates.checkphone);
console.log(validates.checkemail);
```
> `* as`实际上是将导入模块的所有值存放在一个object中，然后可以通过这个object去访问它们



##### 导入时重命名
```js
// test1.js
export let count = 100;  

// test2.js  导入时将count重命名为num
import { count as num } from './test1';

```

##### 导入普通样式
```js
import './style.css';

import styles from './style.css';  // css-module
```

## 二，注意事项

1，普通导出(`export`)时，可以导出object、声明表达式，但不能导出已声明的变量，或者无变量声明的表达式
> 无变量声明，比如匿名函数 function(){...}、class{...} 等等  

!> 总之：export命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系。因为使用import命令的时候，用户需要知道所要加载的变量名或函数名  

```js
const count = 100;  

export count; // 错误❌
export 100; // 错误❌
export function(){}; // 错误❌
export class {}; // 错误❌


export const count = 100; // 正确✔️
export function check(){}; // 正确✔️
export class Component {}; // 正确✔️
export { count }; // 正确✔️
```
  

2，默认导出(`export default`)时，不能导出声明表达式，class除外。  

这是因为export default命令其实只是输出一个叫做default的变量，所以它后面不能跟变量声明语句。  
```js
export default const count = 100; // 错误❌


const count = 100;
export default count; // 正确✔️
export default { count }; // 正确✔️
export default [ count ] // 正确✔️
export default function check(){}; // 正确✔️
export default class Component {}; // 正确✔️
```

3，import导入的变量是只读的
```js
import { a } from './xxx.js'

a = {}; // 错误 Syntax Error : 'a' is read-only;

a.foo = 'hello'; // 合法操作
```