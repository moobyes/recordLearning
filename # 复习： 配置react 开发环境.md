# 复习： 配置react 开发环境

## 主要步骤
1. 生成初步的package.json，整好基础配置
2. webpack 配置，基础配置，环境配置，打包配置等
3. babel 配置，.babelrc配置文件的配置
4. Eslint 配置，.eslintrc 配置
5. sass配置，或者是类似的样式预编译语言配置

基础安装，各类依赖包：

```js

webpack
webpack-dev-server

babel-core
babel-loader
babel-preset-es2015
babel-preset-stage-0
babel-preset-react
css-loader
style-loader
file-loader
url-loader
html-webpack-plugin -D

react
react-dom
react-router-dom
redux 或者其他数据管理依赖，

另外一套：
npm install react react-dom

webpack
webpack-cli
webpack-dev-server
html-webpack-plugin -D

babel-core
babel-loader
babel-plugin-transform-runtime -D

babel-preset-env
babel-preset-stage-0
babel-preset-react -D
```
两个部分非常重要，一个是webpack的配置，一个是babel的配置。拆开来看，先看webpack的配置：

```js
// webpack.config.js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin') // html 插件,负责将html文件虚拟到根目录下
const { CleanWebpackPlugin } = require('clean-webpack-plugin') // 清除之前打包的文件
// 提取css文件
const ExtractTextPlugin = require('extract-text-webpack-plugin')
// 代码压缩
const webpack = require('webpack')


module.exports = {
	// 开发模式，这块也可以配置化
	module: 'development',
	// 入口文件
	entry: './src/index.js',
	// 修改常用模块配置
	resolve: {
		// 自动匹配文件后缀名，引入是不用加文件属性名
		extensions: ['js','.jsx'],
		alias: {
			'test': '/utils/test.js' // 引用这个文件，只需要require('test')
		}
	},
	// 出口文件目录为根目录下的dist，输出文件名为main
	output: {
		path: path.resolve(__dirname, 'dist'),
		filename: 'main.js' // 名字可以配置
	},
	// 配置开发服务器，以及自动更新配置
	devServer: {
		// 基本目录，这里为dist
		contentBase: path.join(__dirname, 'dist'),
		// 自动压缩代码
		compress: true,
		// 配置服务器端口
		port: 3000,
		// 是否自动打开浏览器
		open: true,
		// 其他配置，比如proxy
	},
	// 配置loader
	module: {
		// 配置相应的规则，主要根据文件后缀匹配规则
		rules: [
			// 配置js/jsx语法解析
			{
				test: /\.js|jsx$/,
				use: 'babel-loader',
				exclude: /node_modules/,
				query: {preset:['es2015','stage-0','react']}
			},
			// 配置css语法解析
			{
				test: /\.css$/,
				use: ['style-loader', 'css-loader']
			},
			// 资源配置
			{
				test: /\.(jpg|png|gif|svg|eot|woff|woff2|ttf)$/,use: 'url-loader',
			},
			// 字体转换
			{
				test: /\.(ttf|otf|eot|svg|woff(2)?)(\?[a-z0-9=&.]+)?$/,
				use: 'file-loader'
			}
			// sass，scss 匹配
			{
				test: /\.sass|scss$/,
				// use: ['style-loader','css-loader','sass-loader']
				use: 'style-loader!css-loader!sass-loader' // 从右到左执行
				use: ExtractTextPlugin.extract({
					fallback: 'style-loader',
					use: 'css-loader!sass-loader'
				})
			}
		]
	},
	// 配置相应的插件
	plugins: [
		// html处理
		new HtmlWebpackPlugin({
			// 虚拟的html文件名 index.html
			filename: 'index.html',
			// 虚拟html的模板为 src下的index.html
			template: path.resolve(__dirname, './src/index.html')
		}),
		// 上一次打包代码清理
		new CleanWebpackPlugin(),
		new ExtractTextPlugin({
			filename: 'css/vendor: css',
			disable: false,
			allChunks: true
		}),
		new webpack.optimize.UglifyJsPlugin({
			comments: false, // 是否输出保留注释
			compress: {
				warning: false // 是否打印waring信息
			}
		})
	]
}

```
babel 配置： https://segmentfault.com/a/1190000016458913  6 到7 的踩坑记录，以备参考


