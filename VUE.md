[toc]

# 前端工程化
- 组件化
- 模块化
- 规范化
- 自动化

## Webpack
前端项目工程化的具体解决方案
提供了友好的前端模块化开发支持，代码压缩混淆，处理浏览器端js兼容性，性能优化等

### 初始化项目
1. 新建项目空白目录，运行`npm init -y`命令，初始化包管理配置文件package.json
> `-y`表示都走默认值
2. 新建src源代码目录
3. 新建src->index.html首页和src->index.js脚本文件
4. 初始化首页基本结构(!)
5. 运行`npm i jquery -S`命令，安装jQuery
> -S参数意思是把模块的版本信息保存到dependencies（生产环境依赖）中，即你的package.json文件的dependencies字段中

6. 通过ES6模块化方式导入jQuery`import $ from 'jquery'`

### 安装和配置webpack
`npm i webpack webpack-cli -D`
> -D参数意思是把模块版本信息保存到devDependencies（开发环境依赖）中，即你的package.json文件的devDependencies字段中
>安装时一直卡命令行不动是因为国情的原因，某些网站的访问受到限制，所以下载速度会很慢可能还无法下载所以先安装淘宝镜像再安装webpack
1、安装淘宝镜像`npm config set registry https://registry.npm.taobao.org`
2、安装webpack即可全局webpack安装成功

### 在项目中配置webpack
1. 在项目根目录中创建`webpack.config.js`的webpack配置文件并初始化
```
//Node.js到处语法向外到处webpack的配置对象
module.exports = {
    //mode用来制定构建模式
    //开发用development追求打包速度
    //发布用production追求体积小
    mode: 'development'
}
```
2. 在package.json的scripts节点下新增dev脚本
3. 终端运行`npm run dev`启动webpack进行项目打包构建
> 每次改完代码需要重新打包

#### webpack.config.js
npm run dev运行，读取该配置文件
在webpack4.x和5.x中，有默认约定
- 默认打包入口文件为src -> index.js
- 默认输出文件路径为dist -> main.js
- 可以在webpack.config.js中修改打包的默认约定
> 通过**entry**节点指定打包的入口。通过**output**节点指定打包的出口
```
const path = require('path')    //导入node.js中专门操作路径的模块
module.exports = {
    mode: 'development',
    entry: path.join(__dirname,'./src/index1.js'),  //__dirname: 当前文件所处目录
    output: {
        path: path.join(__dirname,'./dist'),    //输出文件存放地址
        filename: 'bundle.js'   //输出文件名
    }
}

```

### webpack插件

#### webpack-dev-server
- 类似于nodemon(node.js): 自动打包
- `npm i webpack-dev-server -D`
- 配置webpack-dev-server
    1. 修改package.json -> scripts中的dev命令如下
    ```
    "scripts": {
    "dev": "webpack serve"
    },
    ```
    2. webpack.config.js加入
    ```
    devServer: {
    // contentBase: __dirname, -- 请注意，这种写法已弃用
        static: {
          directory: path.join(__dirname, "/"),
        },
    }
    ```
    3. 再次运行`npm run dev`重新打包
    4. 访问`http://localhost:8080`查看自动打包效果
    > webpack-dev-server会启动一个实时打包的http服务器
    > 注意**html文件导入的js文件**应该是**插件生成在内存的bundle.js**而不是文件目录的bundle.js
    
##### devServer节点
在webpack.config.js配置文件中，可以通过devServer节点对 webpack-dev-server 插件进行更多的配置
```
devServer: {
    // contentBase: __dirname, -- 注意，这种写法已弃用
    open: true, //初次打包完成后自动打开浏览器
    host: '127.0.0.1',  //实时打包使用的主机地址
    port: 80,   //实时打包所使用的端口号
    static: {
      directory: path.join(__dirname, "/"),
    },
}
```
    
#### html-webpack-plugin
- webpack中的html插件(类似于一个模板引擎插件)
- 自定制index.html页面内容
- `npm i html-webpack-plugin -D`
```
//1.导入HTML插件得到构造函数
const HtmlPlugin = require('html-webpack-plugin')
//2.创建HTML插件的实例对象
const htmlPlugin = new HtmlPlugin({
    template: './src/index.html',   //指定原文件存放路径
    filename: './index.html'    //指定生成文件存放路径
})
module.exports = {
    plugins: [htmlPlugin]   //3. 通过plugins节点，使htmlPlugin插件生效
}
```
> 复制的index.html存在内存中

### webpack中的loader加载器
webpack默认只能打包处理以.js后缀名结尾的模块。其**他非js后缀名结尾的模块** 
webpack默认处理不了，需要调用**loader加载器**才可以正常打包，否则会报错！

loader加载器的作用：**协助webpack打包处理特定的文件模块**。比如：
- css-loader可以打包处理.css相关的文件
- less-loader可以打包处理.less相关的文件
- babel-loader可以打包处理webpack无法处理的高级JS语法

#### 打包处理css文件
1. 运行`npm i style-loader css-loader -D`
2. webpack.config.js -> module -> rules数组中添加loader规则
```
module: {   //所有第三方文件模块的匹配规则
    rules: [    //文件后缀名匹配规则
        { test: /\.css$/, use: ['style-loader', 'css-loader']}
    ]
}
```
> test表示匹配文件类型，use表示对应要调用的loader
> use数组中指定的loader顺序是固定的
> 多个loader的调用顺序是: 从后往前调用

#### 打包处理less文件
1. 运行`npm i less-loader less -D`
2. webpack.config.js -> module -> rules数组中添加loader规则
```
module: {   //所有第三方文件模块的匹配规则
    rules: [    //文件后缀名匹配规则
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader']}
    ]
}
```

#### 打包处理样式表中与url路径相关文件
1. 运行`npm i url-loader file-loader -D`
2. webpack.config.js -> module -> rules数组中添加loader规则
```
module: {   
    rules: [    
        { test: /\.jpg|png|gif$/, use: 'url-loader?limit=22229'}
    ]
}
```
> ?之后的是loader的参数项
> limit用来指定图片大小，单位为字节byte 
> 只有 ≤ limit大小的图片才会被转为base64格式的图片

#### 打包处理js文件中的高级语法
webpack只能打包处理一部分高级的JavaScript语法。对于那些webpack无法处理的高级js语法，需要借助于**babel-loader**进行打包处理。

1. 运行`npm i babel-loader @babel/core @babel/plugin-proposal-decorators -D`
2. webpack.config.js -> module -> rules数组中添加loader规则
```
module: {   
    rules: [    
        { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/}
    ]
}
```
3. 在项目根目录下创建名为`babel.config.js`的配置文件
```
module.exports = {
    //  声明babel可用的插件
    //  webpack调用babel-loader时，会先加载plugins插件
    plugins: [['@babel/plugin-proposal-decorators', { legacy: true }]]
}
```