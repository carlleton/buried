# ES6相关
## export、exports、modules.exports和require、import的一些组合
**在webpack打包的时候，可以在js文件中混用 require 和 export。但是不能混用 import 以及 module.exports**
否则，会报如下错误
```
“Uncaught TypeError: Cannot assign to read only property 'exports' of object '#<Object>'”
```
来源：[export、exports、modules.exports 和 require 、import 的一些组合套路和坑](http://www.cnblogs.com/CyLee/p/5836069.html)
