# Webpack_demo



### Webpack的基础教程



1. 基础使用
2. 使用HtmlWebpackPlugin
3. 使用WebpackDevServer
4. 编译ES6代码





#### 基础使用

​		创建 package.json 文件

```
npm init -y
```



​		安装 webpack 和 webpack-cli 

```
npm install webpack webpack-cli --save-dev
```



​		根目录下创建src文件夹，接着在里面创建 index.js 文件, 并写个简单的代码 hello word

```
console.log("hello word")
```



​		根目录下创建配置文件 webpack.config.js

```
const path = require('path')

module.exports = {
  mode: 'development',
  entry: path.join(__dirname, 'src', 'index.js'),
  output: {
    path: path.join(__dirname, 'src', 'dist'),
    filename: 'bundle.js'
  }
}
```



​		修改package.json文件 scripts 命令

```
"build": "webpack"
```



​		运行打包 npm run build 



#### 使用HtmlWebpackPlugin

​		安装

```
 npm install html-webpack-plugin --save-dev
```



​		修改配置文件 webpack.config.js

```
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  mode: 'development',
  entry: path.join(__dirname, 'src', 'index.js'),
  output: {
    path: path.join(__dirname, 'src', 'dist'),
    filename: 'bundle.js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, 'src', 'index.html'),
      filename: 'index.html'
    })
  ]
}
```



​		在src目录下新建index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  
</body>
</html>
```



​		再次运行打包  npm run build 



#### 使用WebpackDevServer



​		安装

```
npm install webpack-dev-server --save-dev
```

​	

​		修改配置文件 webpack.config.js

```
devServer: {
    port: 8000,
    static: path.join(__dirname, 'dist')
  }
```



​		修改package.json文件 scripts 命令

```
"dev": "webpack-dev-server"
```



​		 运行  npm run dev 

​		访问  http://localhost:8000/



​		修改 index.html 文件，点击保存， 页面会发生变化



​		

#### 编译ES6代码



​		在 index.js 文件中写一段ES6的代码

```
const sum = (num1, num2) => {
  return num1 + num2
}

console.log(sum(1,2))
```



​		通过查看源代码，可以发现依旧是使用ES6的写法，为了兼容低版本浏览器使用，需要做转化



​		安装 babel

```
npm install @babel/core @babel/preset-env babel-loader --save-dev
```



​		根目录下创建配置文件 .babelrc

```
{
  "presets": ["@babel/preset-env"]
}
```



​		修改配置文件 webpack.config.js

```
module: {
    rules: [
      {
        test: /\.js$/,
        loader: 'babel-loader',
        include: path.join(__dirname, 'src'),
        exclude: /node_modules/
      }
    ]
  },
```



​		通过查看源代码，发现ES6的代码变成了ES5
