Webpack考点「八」-- 常见面试题 ***

目录
> 前端为什么要进行打包和构建？
> module chunk bundle区别
> loader和plugin的区别
> babel和webpack的区别   
> webpack如何实现懒加载   
> 如何产出一个lib       
> babel-polyfill babel-runtime区别    
> 为什么proxy不能被polyfill      
> webpack优化构建速度         
> webpack优化产出代码   
 


#### 前端为什么要进行打包和构建？

代码层面：
* 体积更小（Tree-shaking、压缩、合并），加载更快
* 编译高级语言和语法（TS、ES6、模块化、scss）
* 兼容性和错误检查（polyfill,postcss,eslint）

研发流程层面：
* 统一、高效的开发环境
* 统一的构建流程和产出标准
* 集成公司构建规范（提测、上线）


#### module chunk bundle区别

##### module - 各个源码文件，webpack中一切皆模块
##### chunk - 多模块合并成的
在 entry import() splitChunks 都可以定义chunk:

```
entry: {
  index: path.join(srcPath, 'index.js'),
  other: path.join(srcPath, 'other.js')
},
import('./***/djdj.js').then(res=>{
  console.log(res.data)
})
// splitChunks 代码分割；HtmlWebpackPlugin引用 chunk
```
##### bundle -最终输出文件

#### loader和plugin的区别
loader 模块转换器 （less->css）
plugin 是扩展插件，如HtmlWebpackPlugin

常见的loader和plugin有哪些？
Loader:
* babel-loader：把 ES6 转换成 ES5
* css-loader：加载 CSS，支持模块化、压缩、文件导入等特性
* style-loader：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。
* file-loader (png|jpg|jpeg|gif 开发
* 'url-loader', 生产
* vue-loader

Plugin:
* IgnorePlugin 避免引入无用模块
* HotModuleReplacementPlugin  热更新
* define-plugin：定义环境变量
* commons-chunk-plugin：提取公共代码
* uglifyjs-webpack-plugin：通过UglifyES压缩ES6代码

#### babel和webpack的区别  
babel JS新语法编译工具，只关心语法，不关心模块化
webpack -打包构建工具，是多个Loader plugin的集合

#### webpack如何实现懒加载
import()
* 结合 vue 异步组件 $nexitick
* 结合vue-router异步加载路由 import


#### 如何产出一个lib  
```
output: {
  // lib的文件名
  filename: 'lodash.js',
  // 输出的lib都放到 dist 目录下
  path: distPath,
  // 存放lib的全局变量名称
  library: 'lodash',
},
```
#### babel-polyfill babel-runtime 区别 
babel-polyfill 会污染全局
babel-runtime 不会污染全局，产出第三方lib时要用babel-runtime


#### 为什么 Proxy 不能被 Polyfill 
如 Class 可以用 function 模拟
如 Promise 可以用 callback 模拟
但是 Proxy 功能用 Object.defineProperty 无法模拟

#### webpack优化构建速度
生产环境：
babel-loader
IgnorePlugin
noParse
happyPack
ParallelUglifyPlugin

不能用于生产环境：
自动刷新
热更新
DllPlugin

#### webpack优化产出代码
小图片base64编码 
bundle加hash
懒加载
提取公共代码
使用cdn加速
IgnorePlugin
使用production
Scope Hosting
(场景、效果、原理)
