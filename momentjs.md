## moment.js相关
### moment.js被全量打包
```
// new webpack.ContextReplacementPlugin(/moment[\/\\]locale$/, /zh-cn/),
// new webpack.IgnorePlugin(/^\.\/locale$/, /moment$/),
```
两者选一，官方issues推荐第一种
来自：https://segmentfault.com/q/1010000010575043
