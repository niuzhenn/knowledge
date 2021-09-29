# React-Router
browserHistory和hashHistory
> browserHistory：使用浏览器中的 History API 用于处理 
> hashHistory

路由懒加载
使用React.lazy函数，异步导入组件，再包裹在Suspense内，当路由命中该组件时，才会对该组件进行加载

基于 hash 的路由：通过监听 hashchange 事件，感知 hash 的变化  
改变 hash 可以直接通过 location.hash=xxx  
基于 H5 history 路由：  
改变 url 可以通过 history.pushState 和 resplaceState 等，会将URL压入堆栈，同时能够应用 history.go() 等 API  
监听 url 的变化可以通过自定义事件触发实现  
var _wr = function(type) {
   var orig = history[type];
   return function() {
       var rv = orig.apply(this, arguments);
      var e = new Event(type);
       e.arguments = arguments;
       window.dispatchEvent(e);
       return rv;
   };
};
 history.pushState = _wr('pushState');
 history.replaceState = _wr('replaceState');
上面代码在调用 pushState 的时候回同步 dispatch 一个 pushState 事件，可以监听感知  

react-router 实现的思想：

基于 history 库来实现上述不同的客户端路由实现思想，并且能够保存历史记录等，磨平浏览器差异，上层无感知
通过维护的列表，在每次 URL 发生变化的回收，通过配置的 路由路径，匹配到对应的 Component，并且 render

