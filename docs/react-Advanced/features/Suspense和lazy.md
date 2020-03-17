# Suspense和lazy

React官方提供了`React.lazy`和`React.Suspense`来实现代码分割。  

### React.lazy 

React.lazy允许你将`动态import()`渲染为常规组件。

下面是一个案例：
```js
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <OtherComponent />
    </div>
  );
}
```

> 需要注意的是，目前通过 React.lazy 加载的组件，需要在Suspense里面使用，否则报错

目前`React.lazy`和`React.Suspense`还不支持服务端渲染，如果你使用的是服务端渲染，可以使用[loadable-components](https://github.com/smooth-code/loadable-components)方案。

### React.Suspense

Suspense主要有三个功能：
> 1，配合`React.lazy`实现代码分割

> 2，加载指示符(类似`loading`加载状态)   

> 3，数据获取 (预计在v16.9版本中实现) 

##### 1，结合React.lazy实现代码分割
```js
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <React.Suspense fallback={<div> Loading... </div>}>
        <div>
            <OtherComponent />
        </div>
        </React.Suspense>
    </div>
  );
}
```

##### 2，加载指示符(loading状态)  

调用`Suspense`组件时我们需要给它添加一个`fallback`属性，它的值是一个指示符组件。  

下面是一个案例：
```js
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    // 显示<Spinner> 直到加载其他组件
    <React.Suspense fallback={<Spinner />}>
      <div>
        <OtherComponent />
      </div>
    </React.Suspense>
  );
}
```
> 注意：目前React.Suspense是React.lazy的唯一用例。  






