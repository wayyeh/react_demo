# Spread operator 拓展运算符
 拓展运算符`...`是在对象或数组中展开属性的一种语法。遵循从右往左，相同则覆盖的原则。
### 在对象中使用

```js
 const base = { name:"ben", age:23 };  
  
 // 通过拓展运算符'...'将base属性在user中展开，从而合并对象。
 const user = {  age:20, gender: "男", ...base };  

 console.log(user); // { age:23, gender: "男", name:"ben"};  
```  

##### 在react中的应用  
```js

class UserComponent extends Component {
    render(){
        const user = { name:"ben", age:23, gender: "男" };  
        return <div>
           <Header />  

           <UserPage {...user} />  

           {/* 等同于 */}
           <UserPage name="ben" age="23" gender="男" />  

           <Footer />
        </div>
    }
}  

```  

### 在数组中使用

##### 普通应用 
```js
 const base = [ 1, 2, 3 ];  

 const arr = [ 0, ...base ];  // 数组合并，和concat有相同的功效

 console.log(arr); // [ 0, 1, 2, 3 ]
```
##### `set`和`...`实现数组去重    
ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。
```js
const arr = [ 1,1,2,2,3,4,5,5,5 ]; 
const noRepeatArr = [ ...new Set(arr) ];
```

### 在字符串中使用

```js
 const str = "hello";  

 const arr = [ 0, ...str ];

 console.log(arr); // [ 0, "h","e","l","l","o" ]

```