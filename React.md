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
> 1. getDerivedStateFromProps：
> 2. getSnapshotBeforeUpdate：

# React的setState是同步还是异步的
