# webpack的常用配置
```
{
  mode: '', // 编译目标
  devtool: '', // 生成map
  entry: '', // 入口
  output: {}, // 打包路径
  resolve: {
    extensions: []; // 需要处理的文件后缀
    alias: [], // 别名
    modules: [], // 打包时插件的搜索目录
  },
  module: {
    rules: [], // loader
  },
  plugins: [], // 插件
  optimization: {
    splitChunk: {
      chunks: '',
      cacheGroup: {},
    }
  }
}
```

# 常用loader
file-loader
url-loader
style-loader
css-loader
less-loader
babel-loader
awesome-typescript-loader
react-svg-loader
postcss-loader

# 常用plugin
htmlwebpackplugin
cleanwebpackplugin
mini-css-extract-plugin
happy-pack


# webpack的打包原理
1. 读取webpack的配置文件
2. 启动webpack，创建complier对象并开始解析
3. 从entry配置的入口开始解析，找到依赖的模块，并进行递归解析，形成依赖关系图
4. 对不同类型的文件使用对应的loader进行编译，最终形成javascript文件
5. webpack会向外抛出一些hook，插件可以监听这些事件，并执行插件

