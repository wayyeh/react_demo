# Portals(插槽)

Portals 提供了一种很好的方法，能够将子节点渲染到父组件以外的 DOM 节点。   

Portals主要依赖`ReactDOM.createPortal(child, container)`方法来实现。

<br />

#### ReactDOM.createPortal(child, container)

参数说明：  
> child: 你要插入的`React DOM`，可以是jsx、字符串或者片段 。    

> container: 你要插入的位置，必须是真实存在的`DOM`，比如`body`。

下面是一个案例：  

```js
import React from 'react';
import { createPortal } from 'react-dom';

const Portals = () =>{
    return createPortal(
        <div> 
            给<body></body>插入一段文字
        </div>,
        document.body
    )
}

export default Portals;
```

