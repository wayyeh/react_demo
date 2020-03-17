# 解构赋值    
ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构赋值（Destructuring）。
### 一，对象的解构赋值

#### 基本使用  
对象属性的结构是`key:value`，解构赋值时，变量名需要和属性名`key`一致，否则会是`undefined`。
```js
let user = { name: "ben", age: 20, gender:"男" };  

// 解构赋值
const { name, age } = user;  // 变量名对应的是对象属性的key
console.log(name); // ben
console.log(age); // 20
```
等同于
```js  
// 传统写法
let user = { name: "ben", age: 20, gender:"男" };
const name = user.name;
const age = user.age;

```
案例: 在react组件中应用
```js
class App extends Components {
    render(){
        const { location } = this.props; // 解构赋值
        return <div>
           <p>当前路由是:<span>{ location.pathname }</span></p>
        </div>
    }
}

```

#### 解构时重命名
对象属性是`key:value`结构，因此在解构时，解构出来的变量名默认是该键名key，但我们可以重新命名它。
```js

let user = { name: "ben", age: 20, gender:"男" };

// 解构赋值
const { name: username , age: userage } = user;

console.log(name); // 报错  
console.log(age); // 报错 

console.log(username); // ben   解构时已将变量名改为username
console.log(userage); // 20    解构时已将变量名改为userage
```

#### 解构时设置默认值  

> 设置默认值后，当获取的值不存在时则使用默认值   

```js
// 没有name的user
let user = { age: 20, gender:"男" }; 

// 正常解构赋值
const { name } = user;
console.log(name); // undefined

// 设置默认值
const { name="ben" } = user;
console.log(name); // ben   值不存在时使用默认值
```

### 二，数组的解构赋值  

##### 基本使用  

数组的解构赋值和对象不同，对象解构赋值对应的是键(key)，而数组对应的是索引(Index)
```js
let [first, ,last] = [1, 2, 3];
console.log(first);  // 1
console.log(last);  // 3
```
##### 设置默认值

数组的解构赋值和对象不同，对象解构赋值对应的是键(key)，而数组对应的是索引(Index)
```js
let [ first, , ,last=10 ] = [1, 2, 3];
console.log(first);  // 1
console.log(last);  // 10  // 该数组第四位不存在，因此使用默认值10
```

##### 经典案例：设置多个变量  

当要设置多个变量时，可使用变量解构赋值来简化代码

```js
// 传统写法
let name = "ben";
let age = 23;
let gender = "男";

// 解构赋值写法
let [ name, age, gender ] = [ "ben", 23, "男" ];
```


### 三，字符串的解构赋值    

和数组一样，字符串的解构赋值也是基于下标索引(Index)的。  

```js
const [a, b, c, d, e] = 'hello';

console.log(a); // h
console.log(b); // e
console.log(e); // o
```

### 四，函数的解构赋值    

函数的参数也可以使用解构赋值。    

##### 当参数是`数组`时:
```js
// 原来
function add(args){
  return args[0] + args[1];
}  

// 解构赋值
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3
```

##### 当参数是`对象(object)`时:
```js
// 原来
function add(args){
  return args.x + args.y;
}  

// 解构赋值
function add({ x, y }){
  return x + y;
}

add({ x:1, y:2 }); // 3
```



##### 使用默认值
```js
// 解构赋值
function add({ x=0, y=1 }){
  return x + y;
}

add({ x:1, y:2 }); // 3
add({ y:2 }); // 2
add(); // 1
```