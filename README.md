## 在线的Markdown编辑器
```
http://mahua.jser.me/
```

## Compass
```
官方地址: http://compass-style.org/reference/compass/
```
```
1、Compass是什么？

简单说, Compass是Sass的工具库（toolkit）.
Sass本身只是一个编译器, Compass在它的基础上, 封装了一系列有用的模块和模板, 补充Sass的功能. 它们之间的关系, 有点像Javascript和jQuery、Ruby和Rails、python和Django的关系. 
```

## Compass在Ubuntu下的安装及使用

#### 1、安装
```
$ sudo gem install compass
```

#### 2、创建项目
```
$ compass create testProject // 创建一个testProject项目

执行上面的命令后会在当前目录中就会生成一个testProject子目录. 进入testProject项目目录你会看到, 里面有一个config.rb文件, 这是你的项目的配置文件. 还有两个子目录sass和stylesheets, 前者存放Sass源文件, 后者存放编译后的css文件. 

```

#### 3、编译.
在写代码之前，我们还要知道如何编译. 因为我们写出来的是后缀名为scss的文件，只有编译成css文件，才能用在网站上. 

```
注：所有的命令都是在项目目录下执行，向第二步创建的testProject项目就需要进入testProject中去执行编译命令.
```

Compass的编译命令是：
```
$ compass compile
```

该命令在项目根目录下运行，会将sass子目录中的scss文件，编译成css文件，保存在stylesheets子目录中. 
默认状态下，编译出来的css文件带有大量的注释. 但是，生产环境需要压缩后的css文件，这时要使用--output-style参数. 
```
$ compass compile --output-style compressed
```
Compass只编译发生变动的文件，如果你要重新编译未变动的文件，需要使用--force参数. 
```
compass compile --force
```
除了使用命令行参数，还可以在配置文件config.rb中指定编译模式. 
```
output_style = :expanded
```
:expanded模式表示编译后保留原格式，其他值还包括:nested、:compact和:compressed. 进入生产阶段后，就要改为:compressed模式. 
```
output_style = :compressed
```
也可以通过指定environment的值（:production或者:development），智能判断编译模式. 
```
environment = :development
output_style = (environment == :production) ? :compressed : :expanded
```

在命令行模式下，除了一次性编译命令，compass还有自动编译命令
```
compass watch
```

在命令行下直接使用命令编译生产环境最终使用文件
```
方法一: 直接使用压缩命令重新编译所有文件.
$ compass compile -s compressed --force

方法二: 使用配置文件重新编译所有文件.
$ compass compile -c config_prod.rb --force
```

运行该命令后，只要scss文件发生变化，就会被自动编译成css文件. 
更多的compass命令行用法，请参考官方文档. 


#### 4、实例文件夹如下
```
|-sass
    |-news
        |-news.scss
    |-product
        |-product.scss

|-stylesheets
```

## 项目结构.
```
|-config.rb
|-config_prod.rb
|-sass
    |-main.scss             // 全局样式.
    |-_reboot.scss          // 重置浏览器默认样式.
    |-components            // 【组件】
        |-_components.scss  // 组合所有组件的核心文件.
        |-_alert.scss       // 提示框组件.
        |-_dialog.scss      // 弹出窗口组件.
    |-mixins                // 【混合器】
        |-_mixins.scss      // 组合所有混合气的核心文件.
        |-_box-shadow.scss  // 阴影混合器.
        |-_box-sizing.scss  // 盒模型混合器.
    |-functions             // 【自定义函数】
        |-_functions.scss   // 组合所有自定义函数的核心文件.
        |-_global.scss      // 全局自定义函数.
    |-variables             // 【变量】
        |-_variables.scss   // 全局变量定义.
    |-themes                // 【主题】
        |-_default.scss     // 默认主题.
    |-modules               // 具体模块.
        |-_core.scss        // 模块核心(import变量、混合器、自定义函数……).
        |-domain            // 【域名模块】
            |-domain.scss   // 域名模块

|-stylesheets
    |-main.css              // sass生成.
    |-bootstrap.min.css     // 第三方css框架.
    |-modules               // 模块.
        |-domain
            |-domain.css
    |-vendor                // 第三方插件.
        |-date
            |-date.css
```
