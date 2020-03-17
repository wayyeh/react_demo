# useState - 组件状态管理  

`useState`使函数组件能够使用state。

下面是它的一个基本结构：  

```js
const [state, setState] = useState(initState);
```
> 1，state为你要设置的状态

> 2，setState为更新state的方法，命名随意  

> 3，initState为初始的state，可以是任意数据类型，也可以是回调函数，但必须有返回值

下面是一个具体的例子：
```js
import { useState } from 'react';

const Example = () =>{  
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>你点击了{count}次</p>
      <button onClick={() => setCount(count + 1)}>
        点击
      </button>
    </div>
  );
}
```

