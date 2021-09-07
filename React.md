# React单向数据流
react单向数据流是指数据只能从父组件向子组件传递，并且对于子组件来说，props为只读属性，不可更改
数据的流向只能通过props由外层到内层 一层一层往里传递
单向数据流是react规范的数据流向,它的作用是极大的降低了我们组件间通信的代码耦合，让组件间的通信更为清晰

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

# 避免react重复渲染
props或state改变会触发组件重新渲染（栈内存中的值改变，或者堆内存的指针改变）
1. shouldComponentUpdate
2. React.memo
3. useMemo
4. useCallback
5. getDerivedStateFromProps


# React的setState是同步还是异步的
1. React控制的事件处理程序，以及生命周期函数调用setState为异步更新
2. React控制之外的事件中调用setState是同步更新的，比如原生js绑定的事件，setTimeout/setInterval等

如何控制同步还是异步？

在setState函数中会根据一个变量isBatchingUpdates来确定是同步还是异步，isBatchingUpdates变量默认是false，表示同步更新，另外有一个batchingUpdates函数，在该函数中会把isBatchingUpdates修改为true，在React调用事件处理函数之前会先调用batchingUpdates，把isBatchingUpdates修改为true，则setState就为异步更新

# React组件之间的通信方式
1. 父子组件的通信  
父组件向子组件传值使用props，子组件向父组件通信可以在props中添加回调函数，子组件使用回调函数向父组件传值
2. 跨层级组件通信  
可以通过props一层一层向下传递，但是每层组件都需要写需要传递的值，嵌套太深组件间耦合太严重  
通过context进行通信,使用React.createContext创建一个容器，在数据生产的地方增加一个Provider，在数据消费的地方增加一个Consumer，可跨层级进行数据传递
3. 没有明显关系的组件通信
通过订阅发布模式，在数据消费端添加监听函数，在数据生产端触发监听函数  
通过redux进行数据传递

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

# 循环中添加key的作用是什么
1. 为循环中的元素添加一个唯一的标识，在下次渲染时，react根据key值的变化来判断循环中的元素是否添加，删除，移动的操作，这样react只需要比较循环中的key的变化，不需要一个一个元素进行比较。
2. 防止非受控组件出现渲染错误

# 类组件和函数式组件
1. 函数式组件只是返回一个 React Element。我们渲染一个函数式组件时，只是执行了一次函数，得到了一个React Element，并没有产生实例。
2. 类组件是一个类实例，通过new得来的，只不过我们看不见new的过程而已。当我们渲染类组件时，其实是调用这个类实例的render函数，进而得到一个React Element。
> 类组件性能消耗比较大，因为需要创建实例，但是存在生命周期，state的特性
> 函数式组件只是一个函数，执行完返回一个组件，然后上下文销毁，性能消耗比较小，增加了hooks之后就可以拥有类组件的特性

# 受控组件和非受控组件

# 高阶组件
高阶组件是React中组件的一种模式，它接收一个组件，返回的也是一个组件，是对参数组件的包装，
用处：
> 代码复用
> 渲染劫持
> state抽象
> props修改
应用场景：
1. 子组件功能类似，使用高阶组件进行代码复用
2. 组件功能解耦，把一部分功能抽离到高阶组件内
3. 需要增加功能，又不想改变原有组件逻辑的时候

# hooks
1. useState：为函数组件引入状态
2. useEffect：执行有副作用的代码，第二个参数是一个Array，为函数执行条件，useEffect可以返回一个清除函数，这个函数可以在组件卸载之前运行，也是在每次渲染时清除上一个effect
3. userReducer
4. userContext：组件之间的状态共享
5. useMemo：返回包含函数的结果，并将结果缓存起来，只有当依赖有改变时，才会再次执行useMemo中的代码，返回新的结果
6. useCallback：返回被useCallback包含的函数，并将缓存此函数，只有当依赖参数有改变时，useCallback才会返回一个新的函数
> React.memo()
> 使用React.memo对组件进行包装，当依赖没有改变时，组件不会重新渲染


# React Fiber
之前React的算法，在开始计算dom树之后，整个过程为递归执行，同步执行，无法被打断，如果整个dom树非常大，就会导致页面渲染卡顿，对于用户体验不太友好.
因此，在新版本的React中，将这个过程进行了拆分，分批完成，在一部分完成之后，将控制权交还给浏览器，让浏览器进行渲染，然后在进行下一部分的任务



# React-Redux
React-redux主要解决组件内数据共享问题，对数据进行集中管理，单向数据流
store
> 存储数据
> 包含方法：dispatch（），getStore（），describe（）

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
browserHistory和hashHistory
> browserHistory：使用浏览器中的 History API 用于处理 
> hashHistory

路由懒加载
使用React.lazy函数，异步导入组件，再包裹在Suspense内，当路由命中该组件时，才会对该组件进行加载


