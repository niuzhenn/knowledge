# React的优点，和vue比较有什么不同
1. 通过vdom和diff算法，提高渲染性能
2. 解决了跨浏览器的问题
3. 通过组件，使代码更加模块化
4. 单向数据流，数据更加可控
5. 数据驱动视图，视图和状态一一对应


# React的生命周期
组件加载阶段
> 1. componentWillMount：组件加载时执行，整个生命周期只执行一次，可以在此时setState
> 2. render：创建虚拟dom，进行diff算法，更新dom树
> 3. componentDidMount：组件加载完成时执行，整个生命周期只执行一次，在此时可以获取ref，发送请求

组件更新阶段
> 1. componentWillReceiveProps：只有props更新才会执行，参数为更新后的props，可以在此时去setState
> 2. shouldComponentUpdate：如果返回false，则组件停止更新，可以在此手动控制组件的更新
> 3. componentWillUpdate
> 4. render
> 5. componentDidUpdate：组件更新后调用，参数为上一次生命周期的props和state

组件卸载阶段
> 1. componentWillUnmount：组件卸载前调用，可以在此处做一些清理监听器，清理定时器等
> 2. componentDidUnmount

React的生命周期在V16.4以后做了更改，主要是以下的变更
> 1. getDerivedStateFromProps：参数为props和state，在加载和更新阶段都会调用，返回一个对象来更新状态，或者返回null表示不需要更新
> 2. getSnapshotBeforeUpdate：render之后，渲染完成之前调用，此生命周期返回的任何值都将作为参数传递给componentDidUpdate
> 3. UNSAFE_componentWillMount
> 4. UNSAFE_componentWillReceiveProps
> 5. UNSAFE_componentWillUpdate

# React的setState是同步还是异步的
1. React控制的事件处理程序，以及生命周期函数调用setState为异步更新
2. React控制之外的事件中调用setState是同步更新的，比如原生js绑定的事件，setTimeout/setInterval等

如何控制同步还是异步？

在setState函数中会根据一个变量isBatchingUpdates来确定是同步还是异步，isBatchingUpdates变量默认是false，表示同步更新，另外有一个batchingUpdates函数，在该函数中会把isBatchingUpdates修改为true，在React调用事件处理函数之前会先调用batchingUpdates，把isBatchingUpdates修改为true，则setState就为异步更新

# React的传值方式

# React虚拟DOM
virtul DOM 也就是虚拟节点。通过JS的Object对象模拟DOM中的真实节点对象，再通过特定的render方法将其渲染成真实的DOM节点。

虚拟DOM可以看做一棵模拟了DOM树的JavaScript对象树

在传统的 Web 应用中，我们往往会把数据的变化实时地更新到用户界面中，于是每次数据的微小变动都会引起 DOM 树的重新渲染。
虚拟DOM的目的是将所有操作累加起来，统计计算出所有的变化后，统一更新一次DOM。

# diff算法
React 分别对 tree diff、component diff 以及 element diff 进行算法优化。
1. tree diff
> DOM 节点跨层级的移动操作少到可以忽略不计
> 只对同一层级的节点进行比较，如果节点相同，则更新props，如果不同，则卸载旧节点，加载新节点
2. component diff
> 如果是同一类型的组件，按照原策略继续比较
> 如果是不同类型的组件，则直接卸载旧组件，加载新组件
> 通过shouldComponentUpdate来判断是否需要进行diff
3. element diff
> 同一层级的节点，diff分为三种操作：插入，删除，删除
> 遍历key，如果key相同，无需删除或插入，如果位置有变更，只移动节点，如果位置没变动，只更新节点

# 类组件和函数式组件
1. 函数式组件只是返回一个 React Element。我们渲染一个函数式组件时，只是执行了一次函数，得到了一个React Element，并没有产生实例。
2. 类组件是一个类实例，通过new得来的，只不过我们看不见new的过程而已。当我们渲染类组件时，其实是调用这个类实例的render函数，进而得到一个React Element。
> 类组件性能消耗比较大，因为需要创建实例，但是存在生命周期，state的特性
> 函数式组件只是一个函数，执行完返回一个组件，然后上下文销毁，性能消耗比较小，增加了hooks之后就可以拥有类组件的特性

# 受控组件和非受控组件

# 高阶组件

# hooks
1. useState
2. useEffect：执行又副作用的代码，第二个参数是一个Array，为函数执行条件，useEffect可以返回一个清除函数，这个函数可以在组件卸载之前运行，也是在每次渲染时清除上一个effect
3. userReducer
4. userContext
5. useMemo
6. useCallback

# React Fiber

# React-Redux
store
> 存储数据
> 包含方法：dispatch（），getStore（），describe（），unsubscribe（）

reducer
> 纯函数
> 两个参数：旧的state和action，返回一个新的state

action
> 数据更新从action出发，通过dispatch派发action，action通知reducer发生了什么事件

Provider和connect
Provider：提供包含store的context
connect：连接store和组件

combinReducers：合并多个reducer

mapStateToProps：建立一个从（外部的）state对象到（UI 组件的）props对象的映射关系。
mapDispatchToProps：定义了可以派发action的操作

# React-Router
懒加载
