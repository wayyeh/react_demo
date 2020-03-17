# react组件生命周期

### 基本概念
每个人都有一个生命周期，那就是从出生到死亡。

react组件也有生命周期，从组件初始化到组件渲染完成，再到组件卸载就是一个完整的react组件生命周期。  

> 需要注意的是，class组件自带生命周期，但是函数组件因为是纯函数，需要借助`react hook`才能实现生命周期部分功能。

react组件生命周期主要分为三个阶段，分别是初始化阶段、组件更新阶段、组件卸载阶段。每个阶段都有不同的生命周期方法。

[cinwell website](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram ':include :type=iframe width=100% height=900px')

### Mounting(装载) `初始化阶段` 
一些初始化工作，包括dom渲染，获取数据、填充数据等等。
> 1，constructor  `构造函数`

> 2，static getDerivedStateFromProps() 【新】 `初始化、props或state改变时执行`  

> 3，componentWillMount() / UNSAFE_componentWillMount() 【将废弃】`组件渲染前执行`  

> 4，render() `渲染函数`

> 5，componentDidMount()  `渲染完成后执行`

### Updating(更新) `组件更新阶段`
props或state的改变可能会引起组件的更新，组件重新渲染的过程中会调用以下方法：
> 1，componentWillReceiveProps() / UNSAFE_componentWillReceiveProps() 【将废弃】 `props改变时执行`

> 2，static getDerivedStateFromProps() 【新】 `初始化、props或state改变时执行`  

> 3，shouldComponentUpdate()  `props或state更新时执行`

> 4，componentWillUpdate() / UNSAFE_componentWillUpdate() 【将废弃】 `组件更新前执行` 

> 5，render()  `渲染函数`

> 6，getSnapshotBeforeUpdate() 【新】  `组件更新前执行` 

> 7，componentDidUpdate()  `组件更新完毕后执行` 

### Unmounting(卸载) `组件卸载阶段`  
> componentWillUnmount()  `组件卸载前执行` 

### 错误处理 

> componentDidCatch()  `捕获组件错误信息` 
