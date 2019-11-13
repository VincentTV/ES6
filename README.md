# ES6+ 前端环境

![](https://img.shields.io/badge/language-ES6-yellow.svg) [![LICENSE](https://img.shields.io/npm/l/@eteplus/typeof.svg)](https://github.com/VincentTV/before-after-slider/blob/master/LICENSE) [![](https://img.shields.io/badge/Blog-vincef0ng.cn-brightgreen.svg)](https://vincef0ng.cn)

Webpack 4 + Babel 7 打造 ES6+ 前端环境。

- 指定浏览器兼容 Babel 编译 ES6+ 代码。
- CSS 自动加前缀、压缩、代码文件分离。
- 热模块更新。

## Getting Started

### 下载

```shell
git clone https://github.com/VincentTV/ES6.git
```

### 安装依赖

```shell
cd ES6
```

```shell
npm install
```

### 运行

```shell
npm run start
```
开始 ES6 编程。

### 编译输出

```shell
npm run build
```

```shell
ES6
│
├───dist	
│     ├───assets								
│     │     └───avatar-78c62249.png
│     ├───css
│     │     └───main.css
│     ├───index.html
│     └───main.bundle.js
```

## webpack.config.js

```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const webpack = require("webpack");

module.exports = {
  entry: "./src/main.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "[name].bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: "babel-loader"
      },
      {
        test: /\.css$/,
        use: [
          {
            loader: MiniCssExtractPlugin.loader,
            options: {
              publicPath: "../",
              hmr: true
            }
          },
          {
            loader: "css-loader",
            options: { importLoaders: 1 }
          },
          {
            loader: "postcss-loader",
            options: {
              plugins: [require("autoprefixer"), require("cssnano")]
            }
          }
        ]
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: "url-loader",
        options: {
          limit: 8192,
          name: "assets/[name]-[hash:8].[ext]"
        }
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "src/index.html",
      filename: "index.html"
    }),
    new MiniCssExtractPlugin({
      filename: "css/[name].css"
    }),
    new webpack.HotModuleReplacementPlugin()
  ]
};
```

配置过程及详解，参考个人博客 [Webpack4 + Babel7 打造 ES6+ 前端环境 | Vincent F0ng](https://vincef0ng.cn/post/es6-env/)。