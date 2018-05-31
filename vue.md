# Vue相关
## IE
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
