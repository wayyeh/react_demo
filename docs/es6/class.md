# class 类
> es6中的class(类)是es5原型写法的一个语法糖，拥有很好的开发体验

### 一，基本使用  

```js
// 定义一个空的类
class Point {
}

// 如果class内没有定义constructor，则默认class的constructor为空函数。
class Point {
  constructor() {}
}
```
生成类实例，传递参数
```js
// es6写法
class Point {
  // 构造函数
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}  
// 访问
const a = new Point(1, 2);  
```  
等同于:
```js
// 传统es5写法
function Point(x, y) {
  this.x = x;
  this.y = y;
}
Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};  
// 访问
var p = new Point(1, 2);

```
> constructor是class的构造函数，当使用new生成实例时，constructor方法会自动调用  

### 二，定义class类属性    

##### 1，在constructor内定义
```js  
// es6写法
class Point {  
    constructor() {
        this.state={
            name: null
        }
        this.getname = this.getname.bind(this);
    }
    getname(){
        // do
    }
}    

```    
##### 2，使用[class properties proposal](https://github.com/tc39/proposal-class-fields)定义类属性  
class properties proposal 支持省略constructor，在类内直接定义类的属性，大大简化了类的操作。    
> [class properties proposal](https://github.com/tc39/proposal-class-fields)是es7新提案，
需要[@babel/plugin-proposal-class-properties](https://babeljs.io/docs/en/babel-plugin-proposal-class-properties)插件的支持。  
  
```js
class Point {      

    // 直接定义类属性
    state = {
        name: null
    }    

    // 不再需要在constructor内绑定
    getname(){
        // do
    }
}    
```   
[class properties proposal](https://github.com/tc39/proposal-class-fields)在react中的应用:  
```js
class App extends Component {      

    // 直接定义类属性state
    state = {  
        name: "ben",
        age: 23,
        gender: "男"
    }  

    render(){
        const { name, age, gender } = this.state;
        return <div>
           <p> 当前登录用户: { name }，{ age }岁，{ gender } </p>
        </div>
    }
}
```

### 三，使用`static`定义静态方法和静态属性      
使用static定义类的静态方法，不需要实例化就能访问。
```js
class Point {      

    // static定义静态方法
    static getname(name){
        return name;
    }    

    // static定义静态属性
    static gender = "man";  

    checkphone(){
       // do something
    }
}  

// 访问
const P = Point.getname("ben"); // ben 
const gender = Point.gender; // => man 

```


### 四，在class类内定义函数  
```js
class Point {  
    getname(){
        return 1;
    }
    // 或使用箭头函数
    getname = () =>{
        return 1;
    }
}  
```

### 五，class类的继承  
   
#### 基本使用  
class的继承需要使用`extends`关键字 ，这比 es5 的通过修改原型链实现继承，要清晰和方便很多。
```js
class A {}

class B extends A {
  constructor() {  
    super(); 
    // do
  }
}
```  

#### super的使用 
子类要继承父类，还需要在子类的构造函数内调用super方法，否则会报错。   
super实际上是调用父类的构造函数，但它的this指向的是子类。  
> 注意：super只能用在子类的构造函数之中，并且需要执行`super()`之后才能访问`this`  

```js  
class A {}

class B extends A {
  constructor() {  
    console.log(this); // 报错
    super(); // 继承父类A的属性和方法    
    console.log(this); // 正确
  }
}
```  

#### 使用 [class properties proposal](https://github.com/tc39/proposal-class-fields) 直接继承  
使用class properties proposal的好处是可以省略constructor的繁琐绑定，可以直接定义且自动继承。
```js  
class A {
    state={
        age:23
    }
}

class B extends A {
  state = {
      userage: this.state.age  // age已被继承，因此可直接访问。this指向的是B。
  }
}    

// 访问  
const P = new B();  
console.log(P.state.userage); // 23
``` 