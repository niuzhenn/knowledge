https://segmentfault.com/a/1190000017140200

# 浏览器从输入网址到加载完成过程
1. 输入的如果是域名，需要进行域名解析，拿到域名所对应的ip，浏览器先去缓存里查找，没有就再去系统dns缓存和hosts里面查找
2. 如果再没有找到对应的ip地址，就会向dns服务器发起查询
3. 拿到ip地址以后，浏览器向服务器发起tcp三次握手，建立tcp连接
4. tcp连接建立成功后，浏览器向服务器请求html，css，js，资源文件
5. 浏览器再接收到html文件后，解析html文件并生成dom树，然后解析css，和dom树一起生成渲染树，在渲染过程中会经历重排和重绘，
6. 遇到script标签，会下载解析并执行js文件，浏览器会挂起渲染过程，等js执行完后继续进行渲染

# 跨域
CORS
1. 简单请求
> 使用get,post,head,
> 头部限制:
> 头部增加original字段,说明请求来源
3. 非简单请求: 预检,带方法,和头信息

# http2.0
1. http
> 无状态
> 无连接
> 媒体独立
2. http2
> 支持请求和相应的多路复用
> 压缩头
> 增加请求优先级和服务器推送
> 二进制分帧

# 微前端(前端微服务)
框架: sigleSPA, qiankun
优点:
> 技术栈独立
> 独立开发部署
> 独立运行
> 独立代码库


# 重构
重构条件和重构手法

# 代码检视
1. 编码风格
2. 实现逻辑
3. 复杂度
4. 安全

# 刷新页面怎么保持状态

# git
git init  
git clone  
git pull  
git puush  
git add  
git rm  
git mv  
git status  
git diff  
git commit  
git push  
git reset  
git log  
git blame  
git remote  
git fetch  
git branch  
git merge  
git checkout  
git tag  
