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

# React虚拟DOM

