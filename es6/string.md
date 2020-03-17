# 模板字符串

### 基本使用
  模板字符串是对字符串的一种拓展，它使用``符号定义字符串，并且在字符串内可通过`${ ... }`来使用js表达式。
```js
 const user = { name:"ben", age:23, gender:"男" };   

 let usermsg = `我叫${ user.name }，今年${ user.age }岁，性别${ user.gender }。`;

 console.log(usermsg); // "我叫ben，今年23岁，性别男"  

```  

相当于：  

```js
const user = { name:"ben", age:23, gender:"男" };  
  
// 传统写法
let usermsg = '我叫'+user.name+'，今年'+user.age+'岁，性别'+user.gender+'。';
``` 

### 应用案例:

```js

class App extends Components {
    render(){
        const user = { name:"ben", age:23, gender:"男" };
        let usermsg = `${user.name}，${user.age}岁，${user.gender}`;
        return <div>
           当前用户：{ usermsg }
        </div>
    }
}

// 上面渲染结果:    

 当前用户: ben，23岁，男
```