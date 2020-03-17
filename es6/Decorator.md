# 类修饰器Decorator
修饰器是es7新增的一个特性，主要用于修改class类的行为。[proposal-decorators](https://github.com/tc39/proposal-decorators)

> 修饰器只能用于类和类的方法，不能用于函数。

#### 基本使用  
```js 
// 修饰器函数，它接受class类为参数(target)，并修改类的行为。 
function annotation(target) {  
   target.annotated = true;  // 给MyClass类添加annotated属性
   target.state = {   // 给MyClass类添加state对象
       name:"ben"
   };  
}   

// 使用修饰器时，需要放在类的顶部，或者类方法的顶部，后面不能接符号
@annotation    
class MyClass {   

    // 修饰器也可以用于类的方法
    @annotation 
    getname(name){
        return name;
    }
}
   

console.log(MyClass.annotated); // true
console.log(MyClass.state); // { name:"ben" }
```
> 修饰器函数将类作为参数，并修改类的行为。   

> 修饰器的使用需要[@babel/plugin-proposal-decorators](https://babeljs.io/docs/en/babel-plugin-proposal-decorators)插件的支持。

#### 经典案例——mobx(状态管理器)  
mobx是react生态中主流的状态管理器之一，它应用了修饰器作为store(状态库)和组件之间的粘合剂，使store和组件之间可以很好地交互。
```js
import React, { Component } from 'react';
import { inject, observer } from 'mobx-react';  

// inject表示调用缓存,observer表示当缓存数据生效时，刷新当前页面
@inject("store")
@observer
class SchoolComponent extends Component{  

    state={
        schoolname:this.props.store.school.name // store是通过修饰器注入进来的
    }  

    render(){
        return(
            <div>学校：{ this.state.schoolname }</div>
        )
    }
}
export default SchoolComponent;
```

#### 一些建议  

随着react hook的推出，开发者将更偏向于函数组件，而类组件将会被更少地使用，而修饰器主要应用于类，因此往后修饰器的使用也会减少。

因此不建议大量地使用修饰器，或者可以不使用它。