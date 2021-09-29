# webpack的常用配置
```
{
  mode: 'development | production', // 编译目标
  devtool: 'inline-source-map', // 生成map
  entry: '', // 入口
  output: {
    filename: [name].[contenthash].js,
    path: path.resolve(__dirname, 'dist'),
    publicPath: 'cdn',
  }, // 打包路径
  resolve: {
    extensions: [.ts, .tsx, .js, .jsx, .css, .less, .json]; // 需要处理的文件后缀
    alias: [], // 别名
    modules: ['node_modules'], // 打包时插件的搜索目录
  },
  module: {
    rules: [], // loader
  },
  plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, 'static/index.html'),
    })，
    new MiniCssExtractPlugin(),
  ], // 插件
  optimization: {
    moduleIds: 'deterministic | natural | named | id', // module.id会默认根据解析顺序增加，引用新模块时，导致代码不变，hash改变
    runtimeChunk: 'single', // 提取引导模板，防止代码不变的情况下，hash有所改变
    splitChunk: {
       cacheGroups: {
         vendor: {
           test: /[\\/]node_modules[\\/]/,
           name: 'vendors',
           chunks: 'all',
         },
       },
    }
  },
  devServer: {
    port: 9991,
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        pathRewrite: { '^/api': '' },
      },
    },
    allowedHosts: [],
    client: {
      progress: true,
    },
    headers: {
      'X-Custom-Foo': 'bar',
    },
  },
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
define-plugin

# webpack的作用
1. 模块打包。可以将不同模块的文件打包整合在一起，并且保证它们之间的引用正确，执行有序。利用打包我们就可以在开发的时候根据我们自己的业务自由划分文件模块，保证项目结构的清晰和可读性。
2. 编译兼容。在前端的“上古时期”，手写一堆浏览器兼容代码一直是令前端工程师头皮发麻的事情，而在今天这个问题被大大的弱化了，通过webpack的Loader机制，不仅仅可以帮助我们对代码做polyfill，还可以编译转换诸如.less, .vue, .jsx这类在浏览器无法识别的格式文件，让我们在开发的时候可以使用新特性和新语法做开发，提高开发效率。
3. 能力扩展。通过webpack的Plugin机制，我们在实现模块化打包和编译兼容的基础上，可以进一步实现诸如按需加载，代码压缩等一系列功能，帮助我们进一步提高自动化程度，工程效率以及打包输出的质量。

# webpack的打包原理
1. 读取webpack的配置文件
2. 启动webpack，创建complier对象并开始解析
3. 从entry配置的入口开始解析，找到依赖的模块，并进行递归解析，形成依赖关系图
4. 对不同类型的文件使用对应的loader进行编译，最终形成javascript文件
5. webpack会向外抛出一些hook，插件可以监听这些事件，并执行插件

# devtool的配置项
1. eval: eval 会将每一个module模块，执行eval，执行后不会生成sourcemap文件，仅仅是在每一个模块后，增加sourceURL来关联模块处理前后对应的关系
2. source-map: source-map会为每一个打包后的模块生成独立的sourcemap文件
3. inline: 该属性不会生成独立的 .map文件，而是将 .map文件以dataURL的形式插入
4. cheap: 该属性在打包后同样会为每一个文件模块生成 .map文件，但是与source-map的区别在于cheap生成的 map文件会忽略原始代码中的列信息
5. module: 该属性的配置也是生成一个没有列的信息的sourceMaps文件，同时loader的sourcemap也被简化成为只包含对应行的
6. hidden:
7. nosource:


# hash, fullhash, contenthash

# 如何提高webpack的构建速度
1. 设置合理的sourcemap
2. 使用happypack等插件进行多线程打包
3. 使用loader的时候设置合理的includes和excludes
4. 设置合理的plugin，不设置多余的plugin
5. 合理使用 resolve.extensions(extensions, alias, modules, mainFiles)
6. 使用持久化缓存
7. DllPlugin
8. 使用数量更少/体积更小的 library, splitChunk, treeshaking。
9. 性能开销较大的loader使用cache-loader
10. babel-loader的cacheDirectory

# 如何利用webpack来优化前端性能
1. treeShaking删除不必要代码
2. 代码分割，提取公共代码
3. 懒加载
4. 通过url-loader把小图片转为base64
5. 代码压缩

# plugin和loader的原理

