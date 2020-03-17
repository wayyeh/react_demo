# includes 是否包含

> includes是es7中新增的一个方法，用于在数组或字符串中判断是否包含某个元素，如果包含就返回`true`，否则就返回`false`。

### 在数组中应用
```js
  const arr = [ 1, 2, 3 ];

  console.log(arr.includes(2));  // true
  console.log(arr.includes(9));  // false
```
等同于  
```js
  const arr = [ 1, 2, 3 ];
  // 传统写法
  console.log(arr.indexOf(2)!==-1);  // true
  console.log(arr.indexOf(9)!==-1);  // false
```  

### 在字符串中的应用  

```js
  const str = "Hello world!";

  console.log(str.includes("e"));  // true
  console.log(str.includes("z"));  // false
```
等同于  
```js
  const str = "Hello world!";
  // 传统写法
  console.log(str.indexOf("e")!==-1);  // true
  console.log(str.indexOf("z")!==-1);  // false
```  