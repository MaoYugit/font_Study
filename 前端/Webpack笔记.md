### 1. Webpack简介

#### (1) 定义

 Webpack 是一个用于现代 JavaScript 应用程序的静态模块打包工具。它能够分析项目中的依赖关系，把各种资源（JavaScript、CSS、图片等）打包成一个或多个文件，以便浏览器高效加载和使用。

#### (2) 核心概念

##### **Entry（入口）**

- 入口是告诉 Webpack 从哪里开始构建依赖图的起点。每个依赖图都会有一个或多个入口点。
- 通常，入口文件是项目的主文件（如 `index.js`）。

##### **Output（输出）**

- 输出属性告诉 Webpack 打包文件的输出目录和文件名。
- 默认是 `dist/main.js`，可以在配置文件中进行自定义。

##### **Loaders（加载器）**

- Webpack 本身只理解 JavaScript 和 JSON 文件，加载器让 Webpack 可以处理其它类型的文件（如 CSS、图像、TypeScript 等）。
- 加载器在文件被添加到依赖图中时预处理文件。

##### **Plugins（插件）**

- 插件用于执行范围更广的任务，如打包优化、资源管理、环境变量注入等。
- 常见插件有 `HtmlWebpackPlugin`（生成 HTML 文件）、`CleanWebpackPlugin`（清理输出目录）等。

##### **Mode（模式）**

- Webpack 4 引入了模式配置选项，可以是 `development`、`production` 或 `none`。模式设置会自动地为不同环境进行优化。
- 开发模式包含有用的错误提示和完整的 source map，而生产模式则会启用诸如压缩和 tree shaking 的优化。



### 2. 下载Webpack

#### (1) 下载

```bash
npm i webpack webpack-cli --save-dev
```

简写

```bash
npm i webpack webpack-cli -D
```

​		使用 -D 选项（或者 --save-dev）是为了将依赖项添加到 package.json 文件中的 devDependencies 部分。这样做有以下几个主要原因：通过区分开发和生产依赖，可以确保生产环境中只包含必要的依赖项，减少了项目的体积和复杂度，提高了运行时性能和安全性；
将依赖项正确分类可以帮助其他开发者更容易理解项目的结构和依赖关系。看到一个依赖项在 devDependencies 中，可以立即知道这个依赖项是开发工具，而不是运行时依赖；在 CI/CD 环境中，通常只需要安装生产依赖，而不需要安装开发依赖。这可以通过运行 npm install --production 来实现，它只会安装 dependencies，而跳过 devDependencies。这样可以加快构建过程，减少构建环境中的依赖数量。

#### (2) 配置

在package.json中“scripts”里面加上"build": "webpack --mode=production", 这样下次打包就可以直接用npm run build进行打包

```js
 "scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "build": "webpack --mode=production",
 },
```

```bash
npm run build
```



#### (3) **注意**

由于 npm 的官方源位于国外，下载速度可能会受到网络环境的影响。可以切换到国内的镜像源，比如淘宝的镜像源（cnpm）。

```bash
npm install -g cnpm --registry=https://registry.npmmirror.com
```

之后，可以使用 `cnpm` 代替 `npm` 进行安装：

```bash
cnpm install <package-name>
```

### 

### 3. 修改入口和出口

#### (1) **入口起点(entry point)** 

指示 webpack 应该使用哪个模块，来作为构建其内部 [依赖图(dependency graph)](https://www.webpackjs.com/concepts/dependency-graph/) 的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。

默认值是 `./src/index.js`，但你可以通过在 [webpack configuration](https://www.webpackjs.com/configuration) 中配置 `entry` 属性，来指定一个（或多个）不同的入口起点。例如：

**webpack.config.js**

```js
module.exports = {
  entry: './path/to/my/entry/file.js',
};
```

我改的

```js
module.exports = {
  entry: './src/main.js',
};
```

#### (2) 输出(output)

**output** 属性告诉 webpack 在哪里输出它所创建的 *bundle*，以及如何命名这些文件。主要输出文件的默认值是 `./dist/main.js`，其他生成文件默认放置在 `./dist` 文件夹中。

你可以通过在配置中指定一个 `output` 字段，来配置这些处理过程：

**webpack.config.js**

```javascript
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js',
  },
};
```

我改的

```js
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'app.js',
  },
};
```

在上面的示例中，我们通过 `output.filename` 和 `output.path` 属性，来告诉 webpack bundle 的名称，以及我们想要 bundle 生成(emit)到哪里。path 模块是一个 [Node.js 核心模块](https://nodejs.org/api/modules.html)，用于操作文件路径。



### 4. 生成HTML文件

#### (1) 下载

插件 html-webpack-plugin

```bash
npm install --save-dev html-webpack-plugin
```

或者

```bash
cnpm install --save-dev html-webpack-plugin
```

#### (2) 配置

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
   entry: './src/main.js',
   output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'app.js',
  },
  plugins: [new HtmlWebpackPlugin({
 	template: path.join(__dirname, 'public/index.html'),
  })],
};
```





























































### 11. 打包模式

#### (1) 作用

告知Webpack使用相应模式的内置优化

#### **(2) 分类**

**开发模式**：development  调试代码，实时加载，模块热替换

**生产模式**：production 压缩代码，资源优化，更加轻量

#### (3) 设置方式

**方式1：**在webpack.config.js配置文件设置mode选项（不推荐）

```js
module.exports = {
	// ...
    mode: 'production'
}，
```

**方式2：**在package.json命令行设置mode参数

```js
"scripts": {
	"build": "webpack --mode=production", // 打包用生产模式
     "dev": "webpack serve --mode=development" // 开发用开发模式
}，
```



### 12. source-map配置

#### (1) 作用

代码被压缩和混淆之后，无法正确定位源代码的位置（行数和列数），source map可以准确追踪error和warning在源代码的位置

####  (2) 设置方法

webpack.config.js配置devtool选项

```js
module.exports = {
	// ...
    devtool: "inline-source-map"
}
```

####  (3) 注意

只适用于开发环境，防止被轻易查看源码位置



### 13. 解析别名 alias

#### (1) 作用

配置模块如何解析，创建import或者require的别名，来确保模块引入变得更加简单

#### (2) 方法

原来路径如下：

```js
import { checkUsername, checkPassword } from '../src/utils/check.js'
```

配置解析别名：

```js
module.exports = {
	// ...
    resolve:{
		alias:{
	MyUtils: path.resolve(__dirname, 'src/utils'),
	'@': path.resolve(__dirname, 'src'),
		}
	}
}
```

```js
import { checkUsername, checkPassword } from 'MyUtils/check.js'
```

```js
import { checkUsername, checkPassword } from '@utils/check.js'
```

