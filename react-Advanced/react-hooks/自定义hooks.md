# 自定义hooks  

自定义的hooks是一个 JavaScript 函数，其名称以 `use` 开头，函数内可以调用其他 Hook。

主要就是利用react hooks封装成一个具有特定逻辑的，或可重用的函数。

下面是官方的一个案例，查询指定用户是否在线：
```js
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null); 

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    // 订阅
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      // 组件卸载时取消订阅
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

案例应用：
```js
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```