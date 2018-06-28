# IE相关
## vue
### iview在IE11，关键是微信客户端浏览器报错。
(一）处理iview

在build/webpack.base.conf.js 49行
```js
// 新增iview的babel-loader
{
  test: /\.js$/,
  loader: 'babel-loader',
  include: [...,resolve('/node_modules/iview/src')]
},
```
增加element-dataset
```
$ yarn add element-dataset --save

// 然后在main.js 中新增
import ElementDataset from 'element-dataset'
ElementDataset()
```
（二）处理polyfill
在build/webpack.base.conf.js 24行修改入口
```
entry: {
  app: ["babel-polyfill", "./src/main.js"]
},
```
在src/main.js
```
import 'babel-polyfill'
```
摘自：https://blog.csdn.net/u010377383/article/details/79944214

### 在IE11中，字符串形式的template中不能使用ES6语法，即使使用polyfill也不行
解决方法是把相应的处理放到computed或者filters中，这样polyfill可以处理它，template是字符串，IE11不能解析ES6的语法

### canvas中svg的图片，可以正常绘制，但获取`getImageData`总是报`SecurityError`
换成`.png`解决

### IE下put操作，如果只有一个url，数据为空时，提交会报`Unhandled promise rejection`
将`put(url)`改为`put(url, {})`

### IE9+下svg的polyfill
使用[svgxuse](https://github.com/Keyamoon/svgxuse)来兼容IE9+