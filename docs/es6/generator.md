# generator异步编程  
### 一，基本简介
和promise一样，generator也是一种异步处理方案。  

但generator做得更彻底，它能实现以同步的方式来处理异步，过去处理异步可能需要十几行代码，而它只需要一行代码。  
```js
 // 传统回调式异步处理  -  回调地狱
 ajax('http://url-3', options, function (err, result) {
      if (err) {
          return alert(err);
      }
      // 做一些事情
      ...
  });
  

 // generator处理异步
 function* (){
    ...
    const result1 = yield fetch('http://url-1');
    const result2 = yield fetch('http://url-2'); 

    console.log(result1);
    console.log(result2);
    ...
 }
```

### 二，generator基本使用    

##### 1，Generator函数和普通的函数区别
> a，function和函数名之间有一个*号  

> b，函数体内使用了yield表达式    

##### 2，定义generator函数      
 定义generator函数需要使用`fuction*`关键字，函数内可使用`yield`等待处理异步操作。
 > 注意： yield后面通常要接promise   

```js
  function* fn(){
      const result = yield fetch('./post.json'); // 执行完后才会执行下一行代码，感官上相当于同步
      console.log(result);
  }
```  
在对象或class中定义可简写：  
```js
  // 在对象中定义  
  const obj = {
    username: "ben",
    * fn(){
        const result = yield fetch('./post.json'); 
        console.log(result);
    }
    // 或
    *
  }  

  // 在class中定义  
  class App {  

    * fn(){
        const result = yield fetch('./post.json'); 
        console.log(result);
    }
  }
```

##### 3，generator原生用法  
调用generator对象有两个方法:    

一是不断地调用generator对象的next()方法  

二是直接用for ... of循环迭代generator对象
```js
 function* fn(){
    const res = yield fetch('./post.json');  // 同步执行
 }  
  
// 1，使用next调用generator函数
const g = fn();
const result = g.next();  

result.value.then(function(data){
  return data.json();
}).then(function(data){
  g.next(data);
});    
  

// 2，使用`for of`调用generator函数，遍历出来的是promise实例
for (let p of fn()) {  
  console.log(p);
}

```  

### 三，使用co模块简化generator操作    
co是一个js模块，它对generator做了很多封装处理，它能自动执行generator函数，大大简化了generator的操作流程。
> 使用co时，yield后面必须是promise   

```js
// co方法接收generator作为参数
co(function *(){
  try {
    const result = yield fetch('./post.json');  // 同步执行
    console.log(result);
  } 
  catch (err) {
    console.error(err);
 }
})
.catch(err=>{
    console.log(err);
});

```

