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

# 常用plugin

