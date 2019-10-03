基本配置
# 1 入口[entry]
webpack就以这个初始js文件为「入口」，根据代码中声明的模块引用来加载其他资源文件，根据webpack配置来对加载的模块进行编译、打包，最终「输出」开发人员期望的打包结果。

```js
module.exports = {
  entry: {
    pageA: './pageA.js',
    pageB: './pageB.js'
  }
};


//entry也可以为数组，如：

module.exports = {
  entry: ['./fileA.js', './fileB.js']
};
// 也可以这样：
module.exports = {
  entry: {
    main: ['./fileA.js', './fileB.js']
  }
};

```
# 2 出口[output]
我们所定义的「入口」是开发时的程序入口，最终编译构建后，真正被浏览器加载的资源文件则是「出口」文件。「出口」的相关配置定义了输出文件的路径与文件名。最基本的配置为：

```js
module.exports = {
  output: {
    filename: 'output.js', // 文件名
    path: __dirname + '/dist' // 文件输出路径，必须为系统绝对路径
  }
};

//由于「入口」会存在多个，同样的「出口」文件也会有多个，多出口的定义如下：

module.exports = {
  entry: {
    pageA: './a.js',
    pageB: './b.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
};

```

# 3 模式[mode]
模式是webpack@4新增的配置属性，目的是为了简化webpack繁琐的配置。在一个工程化的项目中：生产环境下，我们希望输出的文件是经过压缩、混淆（丑化）的。而开发环境时由于调试需要，我们希望文件是未压缩与混淆的。

在webpack@4以前，我们往往通过执行不同的npm script命令，从而设置不同的process.env.NODE_ENV，进而在webpack配置文件中判断此时环境变量，加载不同的webpack插件，输出不同的配置。

由于大部分工程项目的开发环境与生产环境有着较为统一的需求，因此webpack@4+通过配置不同模式[mode]，来默认执行该模式下的一些通用操作。如生产模式时，默认引入代码压缩混淆插件 UglifyJsPlugin 与作用域提升的插件 ModuleConcatenationPlugin 。

目前已有的模式有：production 、development 、none ，默认为production。设置为 production 与 development 时会同时默认设置process.env.NODE_ENV为production或development。 设置 none 时，webpack不做任何附加操作。

# 4 模块[module]
我们知道webpack 是一个模块打包器，它不仅仅能处理js文件，还能处理css、图片。而且也能将ES6的代码、甚至是TypeScript的代码引用并打包输出成当下可执行的js文件。而webpack自身不可能穷举处理所有的相关文件。于是就采用了 loader 方式。

    loader 用于对模块的源代码进行转换。loader 可以使你在 import 或 "加载" 模块时预处理文件。

不同的文件类型可能需要匹配不同的loader，做不同的文件转化。而有的模块可能需要处理，有的模块可能需要忽略，这一切相关的配置就在 module 中。