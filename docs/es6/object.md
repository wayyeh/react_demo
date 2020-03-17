# 对象拓展

### 一，对象属性简写   

##### 基本使用
```js
let name = "ben";
let age = 23;
let gender = "男";   

// 赋值给user变量，使用简写的形式
const user = { name, age, gender  };
  

// 实际上等同于:
const user = { 
    name: name,
    age: age,
    gender: gender
}
```

##### 函数简写  
```js    
let name = "ben";
let age = 23;
const user = {
    name,
    age,  
    // 函数简写
    auth(name){
        return !name;
    }
}

```  
实际上等同于   

```js    
let name = "ben";
let age = 23;  
// 传统写法
const user = {
    name: name,
    age: age,  
    auth: function(name){
        return !name;
    }
}

```  

##### 使用拓展运算符`...`
```js

// 赋值给user变量，使用简写的形式
const base = { name:"ben", age:23 };   

// 使用`...`
const user = { ...base, gender:"男" }
console.log(user);  // { name:"ben", age:23, gender:"男" }

```


### 二，Object.keys()  

对象属性是`key:value`结构，而Object.keys()方法主要用于把对象属性的键`key`转成一个数组。     

```js
const user = { name:"ben", age:23, gender:"男" };

const userkey = Object.keys(user);

console.log(userkey);  // [ "name", "age", "gender" ]

```  


##### 经典案例:
```js

class App extends Component {
    render(){
        const user = { name:"ben", age:23, gender:"男" };
        const options = { name:"用户名", age:"年龄", gender:"性别" };
        return <div>
           {
               Object.keys(options).map(function(key){
                   return <p key={key} >  
                      { options[key] } : { user[key] }
                   </p>
               })
           }
        </div>
    }
}

// 上面渲染结果:  

用户名: ben
年龄: 23
性别: 男

```

### 三，Object.values() 

和Object.keys()不同，Object.values方法主要用于把对象属性的值`value`转成一个数组。     

> Object.values是es7中新增的方法

```js
const user = { name:"ben", age:23, gender:"男" };

const uservalue = Object.keys(user);

console.log(uservalue);  // [ "ben", 23, "男" ]

```


### 四，Object.assign() 

这是一个对象合并的方法。从右往左合并，当遇到相同属性时会直接覆盖。  

```js
const base = { name:"ben", age:23 }; // 基本信息
const expand = { age: 20, gender:"男", birthday:"1月1日" }; // 额外信息

// 对象合并
const user = object.assign(base,expand)
console.log(user);  // { name:"ben", age: 20, gender:"男", birthday:"1月1日" }
```
> base和expand都有age属性，但expand在右边，合并是从右往左的，所以expand的age覆盖了base的age

### 五，Object.entries() 

这是一个对象属性迭代的方法，最终产生一个二维数组。二维数组中的每个属性对应对象属性的`key`和`value`。

```js
const user = { name:"ben", age:23};

// 对象属性迭代
console.log(Object.entries(user));  // [ ["name","ben"],["age",23] ]
```
相当于:
```js
const obj = { 
    key:value 
};

// 对象属性迭代
console.log(Object.entries(obj));  // [ [key,value] ... ]
```

### 六，Object.is() 

Object.is()用于判断两个值是否相等，与运算符`===`等效。

```js
Object.is('foo', 'foo')
// true  

Object.is({}, {})
// false
```
  
> 如果要判断两个对象是否相等，建议使用lodash的isEqual方法  

```js  
import _ from 'lodash';  

let object = { 'a': 1 };
let other = { 'a': 1 };
 
_.isEqual(object, other);
// => true
 
object === other;
// => false
```