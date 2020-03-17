# 额外的Hooks

* useMemo  
* useCallback  
* useRef  
* useImperativeMethods  
* useLayoutEffect   

## useMemo    

useMemo是一个用于性能优化的API，它通过`记忆值`手段让你避免在每个渲染上执行高开销的计算，可减少渲染的耗时。

尤其适合用在需要复杂计算的场景，比如`复杂的列表渲染`，对象深拷贝等等。

##### 基本用法  
```js
const memoizedValue = useMemo(callback,array);
```
> 1，callback： 一个函数，用于处理你的计算逻辑。      

> 2，array： 一个数组，当数组发生改变时useMemo才会重新执行。     

useMemo的返回值是一个记忆值，它是callback的返回值。  

useMemo只会在数组发生变化时才会重新计算memoized(记忆)值。这样的优化有助于避免在每个渲染上进行昂贵的计算。

下面是一个用例：  
```js
// useMemo只会在obj1或obj2发生改变时才会重新执行。 

const obj1 = { id:"12", name:"jack" };
const obj2 = { id:"14", name:"ben", age:23 };

const memoizedValue = useMemo(()=>Object.assign(obj1,obj2),[obj1,obj2]);

// 使用
<div> { memoizedValue.name } </div>
```

> 注意：不要在useMemo里面处理副作用的逻辑，副作用应该放在useEffect内处理。   

<br/>      
## useCallback  
useCallback和useMemo一样，都是用于性能优化的API。
##### 基本用法  
```js
const memoizedCallback = useCallback(callback,array);
```  
> 1，callback： 一个函数，用于处理你的计算逻辑。      

> 2，array： 一个数组，当数组发生改变时useCallback才会重新执行。      

useCallback 和 useMemo 类似，它们的返回值都是记忆化的。但是会有一些不同，useMemo的返回值就是callback的返回值，而useCallback的返回值则callback函数本身。    

`useCallback(fn, inputs)` 等价于 `useMemo(() => fn, inputs)`。
   
<br/>    

下面是useCallback一个案例：
```js
const obj1 = { id:"12", name:"jack" };
const obj2 = { id:"14", name:"ben", age:23 };

const memoizedFn = useCallback(()=>Object.assign(obj1,obj2),[obj1,obj2]);  

// 使用
<div>{ memoizedFn().name }</div>
```
它相当于useMemo的这种写法：  
```js
const obj1 = { id:"12", name:"jack" };
const obj2 = { id:"14", name:"ben", age:23 };

const memoizedFn = useMemo(()=>{
    return ()=>{
        return Object.assign(obj1,obj2)
    }
},[obj1,obj2]);  
// 或
const memoizedFn = useMemo(()=>()=>Object.assign(obj1,obj2),[obj1,obj2]);

// 使用
<div>{ memoizedFn().name }</div>
```
<br/> 

## useRef  

useRef 返回一个可变的 ref 对象，其 .current 属性被初始化为传递的参数（initialValue)。

基本用法:  
```js
const MyComponent = () =>{
    // 1，创建ref
    const inputEl = useRef(null);
    const onInput = () =>{
        // 3，访问ref
        console.log(inputEl.current.value)
    }
    // 2，挂载ref
    return (
        <div>
            <input ref={ inputEl } type="text" />
            <p>
                <button onClick={ onInput } > 获取input的值 </button>
            </p>
        </div>
    )
}
```

<br/> 

## useImperativeMethods

useImperativeMethods是一个用于拓展ref实例的API，它能够让你自定义`使用 ref 时公开给父组件的实例值`。

下面是它的一个用例：  
```js
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeMethods(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />;
}
FancyInput = forwardRef(FancyInput);
```

<br/> 

## useLayoutEffect 
useLayoutEffect 与 useEffect 基本相同，但它在所有 DOM 变化后同步触发。 它能够从 DOM 读取布局并同步重新渲染。 在浏览器有机会绘制之前，将在 useLayoutEffect 内部计划的更新将同步刷新。

在多数情况下首选标准的 useEffect ，以避免阻止视觉更新。  

下面是useLayoutEffect 的一个案例：
```js
useLayoutEffect(() => {
    const rootEl = document.getElementById("root");
    console.log(rootEl.);
  },[])
```
