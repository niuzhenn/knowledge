
# React-Redux
React-redux主要解决组件内数据共享问题，对数据进行集中管理，单向数据流

Redux遵循的规则
> 单一数据来源：数据存放在store中
> 状态只读：只能通过触发action来修改状态
> 状态可预测：使用纯函数更改状态

store
> 存储数据
> 包含方法：dispatch（），getStore（），describe（）

reducer
> 纯函数
> 两个参数：旧的state和action，返回一个新的state

action
> 数据更新从action出发，通过dispatch派发action，action通知reducer发生了什么事件

redux的实现流程
1. 用户通过页面上的事件，调用dispatch，触发action
2. store自动调用reducer，传入当前state，收到的action，reducer返回新的state
3. state更新后，store就会调用监听函数，根据state触发重新渲染，更新view

Provider
> 提供包含store的context

connect
> 连接store和组件
> 包装原组件：将state,action通过props的方式传入到原组件内部
> 监听store tree变化：使其包装的原组件可以响应state的变化

combinReducers
> 合并多个reducer

mapStateToProps
> 建立一个从（外部的）state对象到（UI 组件的）props对象的映射关系。

mapDispatchToProps
> 定义了可以派发action的操作


### redux中间件是什么，中间件的执行过程？
中间件的使用（改变数据流）：

未使用redux: action-> reducer
使用redux: 自定义拦截，变成 action->middlewares->reducer
实现如异步action,action过滤，日志输出，异常报告等功能；

使用： redux提供的一个方法： applyMiddleware，可应用多个中间件；

### redux常用中间件
redux-logger
redux-thunk

### redux的hooks
useDispatch：获取dispatch方法
useStore：获取store
useSelector：访问store中的数据，参数是一个函数，可以在函数里对数据进行二次包装
