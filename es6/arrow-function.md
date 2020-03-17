# 箭头函数
es6 允许使用“箭头”（=>）定义函数，给开发者带来大大的便利。
### 一，基本使用  

```js  
 // 匿名箭头函数
 (arg) =>{
     // Todo
 }    
 
 // 有名箭头函数
 const fn = (arg) =>{
     // Todo
 }
```  
等同于:  
```js  
 // 传统写法
 function fn(arg){
     // Todo
 }
```   
> 注意：匿名箭头函数不能直接定义，它需要依附，比如作为回调函数  arr.forEach((item)=>{ ... })
  
### 二，多种写法  
  
##### 不同参数  
```js  
 // 单个参数时，可省略括号()
 const fn = arg =>{
     // Todo
 }  

 // 没有参数或有多个参数时，需要加括号() 
 const fn =()=>{
     // Todo
 }  
 const fn =(arg1,arg2...)=>{
     // Todo
 }    
```     

##### 不同返回值    
1，单条语句返回值时，可省略大括号{} 
```js  
 // 单个参数
 const fn = v =>v;  
 
 // 多个参数
 const fn = (x,y) =>x+y;  
```    
2，多条语句返回值时，需要加大括号{} 
```js  
 const fn = v =>{
    if(v){
        return v++;
    }
 };  
``` 
3，单条语句且返回值为对象时，可省略大括号{}，但返回值需要用()包裹。
```js  
 const fn = user =>({ id: user.id, name: user.name });  
 //等同于  
 function fn(user){
    return {
        id: user.id, 
        name: user.name
    }
 }  
``` 

##### 使用解构赋值  
1, 参数为object时
```js
// 原来
const fn = user =>({ id: user.id, name: user.name });   

// 使用解构赋值  
const fn = ({ id, name, age, gender }) =>({ id, name });

```  
2, 参数为数组时
```js
// 原来
const fn =arr=>arr[0]+arr[0];   

// 使用解构赋值  
const fn = ([x,y]) =>x+y;

```

### 三，箭头函数嵌套    

1，没有函数嵌套时
```js    
const fn= a =>a;    

//等同于
function fn(a){
   return a;
}
```
2，一层函数嵌套时
```js    
const fn= a =>b=>a+b;    

//等同于
function fn(a){
   return function(b){
       return a+b;
   }
}
```
3，两层函数嵌套时
```js    
const fn= a => b => c =>a+b+c;    

//等同于
function fn(a){
   return function(b){
       return function(c){
           return a+b+c;
       };
   }
}
```
4，三层函数嵌套时
```js    
const fn= a => b => c => d =>a+b+c+d;    

//等同于
function fn(a){
   return function(b){
       return function(c){
           return function(d){
               return a+b+c+d;
           }
       };
   }
}
```

> 以此类推...