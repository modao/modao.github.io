title: "重新学习js模块规范"
date: 2015-03-29 10:16:03
tags: blog
---

## 背景
* 团队前端技术选型定的是使用KISSY5 modulex作为基础框架，该框架使用define语法来定义模块，故研究下define的各种模块规范写法

## KISSY5支持的模块写法
- commonjs写法(define(modName, modDeps, factory))，示例如下
```
    define('name', ['node'], function(require, exports, module){
        var Node = require('node');
        module.exports = function(){
            //do sth
        };
    });
```
推荐使用书写时隐去模块名+依赖，使用gulp-kmc打包
```
    define(function(require, exports, module){
        var Node=require('node');
        module.exports=function(){
            //do sth
        };
    });
```
- kmd写法（define(modName, factory, modDeps)），示例如下
```
    define('name', function(Node, IO){
    //do sth
    }, {'requires': [
        'node',
        'io'
    ]});
```
不推荐使用这种书写方法，这是kissy独有的模块规范，不成社区标准


## 模块规范

### AMD规范
* AMD是Asynchronous Module Definition的简写，中文名异步模块定义。主要是为了解决js模块同步载入阻塞浏览器渲染以及模块间依赖不好处理的问题。
* AMD规范模块写法（define(modName, modDeps, factory)），示例如下
```
    define('name', ['node', 'io'], function(Node, IO){
        //do sth
    });
```
* AMD规范实现典型例子requireJs，其要求所有模块为一个独立的文件，主要有两个全局变量define和require。模块定义使用define方法，示例如下：
```
    define(['node', 'io'], function(Node, IO){
        //do sth
        return sth;
    });
```
调用模块使用require语法，示例如下：
```
    require(['modA, modB'], function(ModA, ModB){
        //do sth with ModA&ModB，no return
    });
```
其中modA，modB这些require载入的模块名称对应的路径是通过require.config来指定路径的，这样才能够在define定义的模块中省去模块名，示例如下：
```
    require.config({
        'baseUrl': 'http://g.tbcdn.cn/crm/',    //baseUrl也可以为相对路径，为相对当前文件的路径
        'paths': {
            'modA': 'modA',
            'modB': 'modB',
            ...
        }
    });
```
require.config一般配置在入口js文件的开始部分，入口js文件是通过静态载入require.js中通过data-main属性指定的，示例如下：
```
    <script src="js/require.js" defer async="true" data-main="js/main.js"></script>
```
AMD规范中也提供了兼容CommonJs的写法
* 参考文章：
    * [requireJs的用法](http://www.ruanyifeng.com/blog/2012/11/require_js.html)
    * [requireJs官网](http://requirejs.org/)
    * [amdjs规范](https://github.com/amdjs/amdjs-api/wiki)

### CMD规范
* CMD是Common Module Definition的缩写
* CMD模块的书写规范：
```
    define( 'module', ['module1', 'module2'], function( require, exports, module ){
        // 模块代码
    } );
```
* 对其中的参数说明：
    * require用来进行依赖模块加载，可以实现同步加载与异步加载
```
    var Node=require('node');   //同步加载
    require.async('./a', function(a){       //异步加载
        //do sth with a
    });
```
    * exports用来定义模块对外提供的接口
```
    define(function(require, exports, module){
        exports.param=param;
        exports.init=function(){
            //do sth
        };
    });
```
或使用return来提供对外接口
```
    define(function(require, exports, module){
        return {
            'param': param,
            'init': function(){
                //do sth
            }
        };
    });
```
或使用module.exports来提供对外接口
```
    define(function(require, exports, module){
        module.exports = {
            'param': param,
            'init': function(){
                //do sth
            }
        };
    });
```
    * module为一个存储模块相关一些信息的对象，例如：
        * module.id 为模块的唯一标识。
        * module.uri 根据模块系统的路径解析规则得到模块的绝对路径。
        * module.dependencies 表示模块的依赖。
        * module.exports 当前模块对外提供的接口。

### CommonJs规范
* CommonJs规范实质上也是一整套规范(包括模块化、文件处理、IO stream、socket等一系列规范)，它不只是限于模块规范的定义，有点类似与ECMAScript规范分庭抗礼的感觉（ECMAScript定义浏览器端js应该有的语言特性与API，CommonJs定义服务端js应该有的语言特性和API）。nodejs为部分实现CommonJs规范的典范
* CommonJs模块规范中的一个文件就是一个模块，模块里面有require和exports两个可以直接使用的方法。其中require用来载入另外一个CommonJs模块，
exports用来定义模块输出。示例代码
```
    //addition.js
    exports.message='add';
    exports.add=function(a, b){
        return a+b;
    }
```
载入模块：
```
    var add=require('./addition');
    console.log(add.message);
    add.add(1, 2);  //3
```
如果模块返回仅为一个函数，可以使用module.exports。（注意这里与CMD规范不同）
```
    //addition.js
    module.exports = function(a, b){
        return a+b;
    };
```
* 参考资料：
    * [commonJs官网](http://www.commonjs.org/)
    * [http://arstechnica.com/business/2009/12/commonjs-effort-sets-javascript-on-path-for-world-domination/](http://arstechnica.com/business/2009/12/commonjs-effort-sets-javascript-on-path-for-world-domination/)