# React-Redux hooks
### useSelector()
```
const result : any = useSelector(selector : Function, equalityFn? : Function)
```
通过传入 selector 函数，你就可以从从 Redux 的 store 中获取 状态(state) 数据。

### useDispatch()
这个 hook 返回 Redux store 的 分发(dispatch) 函数的引用。你也许会使用来 分发(dispatch) 某些需要的 action。

### useStore()
这个 hook 返回传递给 组件的 Redux sotore 的引用。

# Redux的中间件
1. redux-log
2. redux-thunk
3. redux-actions

redux的中间件
1. 在不使用中间件时，dispatch一个action以后，会调用reducer，然后根据action的type返回新的state
2. 使用中间件以后，dispatch一个action，会先交给中间件处理，然后再交给reducer执行
