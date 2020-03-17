# hooks的规则

Hooks 是 JavaScript 函数，但在使用它们时需要遵循一些规则。

### 只在顶层调用Hooks

尽量在顶层作用域中调用Hooks。

不要在循环，条件或嵌套函数中调用Hook，否则可能会无法确保每次组件渲染时都以相同的顺序调用Hook。

### 只在函数组件中调用Hooks

React Hooks目前只支持函数组件，因此你不能在class组件中调用它API，但你可以在class组件内调用react hooks组件。  

下面是React Hooks的应用场景：

> 1，函数组件    

> 2，自定义hooks (在自定义的hooks中调用hooks)

在未来，react官方计划将`React Hooks` 拓展到class组件，到时候class组件也能使用`React Hooks`。
