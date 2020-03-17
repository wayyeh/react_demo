# let 和 const的用法
## 一，基本使用
```js
// 定义count 

// es5写法  
var count = 100;

// es6写法
let count = 100;

// 使用const定义常量count 
const count = 100;
```
> 注意：常量是不可变的，也就是常量定义之后不能更改它，否则会报错  

!> 建议：尽量使用const，除非值可变(值可变时使用let)

## 二，注意事项

##### 块级作用域
```js
// es5 - var作用于全局作用域和函数作用域
function f1() {
  var n = 5;
  if (true) {
    var n = 10;
  }
  console.log(n); // 10
}

// es6 - let只作用于它所在的块级作用域
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
```

##### 不允许重复声明
let不允许在同级作用域内，重复声明同一个变量。
```js
// es5 
function f1() {
  let count = 100;
  let count = 10; // 会报错
}
```


##### 不存在变量提升

```js
// var 的情况
console.log(count); // 输出undefined
var count = 2;

// let 的情况
console.log(count); // 报错ReferenceError
let count = 2;

```
