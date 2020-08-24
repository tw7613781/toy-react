学习过程中的一些笔记

# 1. webpack

## 1.1 介绍

webpack是前端常用到的打包工具。输入是一些js文件，输出也是js文件。即把多个js文件打包成单个js文件。

一般是由单个js为入口，通过import或require一些东西后，最终变成一个单一的大文件。比较符合我们在web上的性能和发布的需求

webpack也会用到其他的工具，其中babel是常用到的，是以loader的形式使用的。

> babel是个把新版本js文件翻译为老版本js文件的一种工具

> webpack loader；原则上webpack只能打包js文件。如果webpack想把css文件打包进入js文件，那么就需要个css loader。如果webpack想把html文件打包进入js文件，那么就需要个html loader。如果webpack想把一些语法比较新的js打包进入js文件，并且为了提高兼容性，要把它变为版本比较旧的就是文件，那么就可以使用babel loader.loader可以是独立的npm包。所以说babel使用loader去定制各种各样的文件。

## 1.2 安装

需要安装webpack和webpack-cli两个包

## 1.3 配置

在根目录下创建webpack.config.js文件

因为我们不会使用babel对webpack的confi文件做转换，所以我们最好就用es5的`module.exports`的写法来输出这个文件

```
module.exports = {

}
```

主要有以下各种配置属性

- entry：即使前面介绍部分提到的入口文件。webpack是从这里开始读入js文件以及通过它对其他包的引用完成所有js文件的输入的

- module属性里面重要的就是rules，rules是个数组，里面是一条一条的规则。

- rule里面的每一条规则是由test和use组成。test是个正则表达式，所有匹配了这个正则表达式的文件都可以使用use里面的设定。

- use里面就有loader属性了，这里我们为了打包使用新语法的文件，可以配置babel loader。loader的配置是用options属性来加入的。这里就是用babel预设定的preset设定了。而要让babel获得解析jsx文件的能力，需要配置一个babel的plugins，叫做@babel/plugin-transform-react-jsx，在安装了相应的包之后，在presets的下面添加plugins属性，它也是一个数组，把刚安装的这个包的名字加入就行了。而对这个plugin的配置，可以通过它的pragma属性进行。

> 这里需要安装babel-loader, @babel/core, @babel/preset-env（babel预设的配置）

- mode: "development"

- optimization

  - minimize: false

- 上面这两个属性的配置是让打包后的代码具有可读性。当然这只是在开发模式下的配置。

## 1.4 执行

因为我们的webpack不是使用`-g`来全局安装的，所以这里可以使用一个`npx`来执行我们的webpack

> 使用npx命令可以使用安装在本地的（不是全局的）可执行脚本。

```
npx webpack
```

# 2. JSX

jsx的本质就是在js中能够写html语句。