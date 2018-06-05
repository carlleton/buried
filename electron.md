# electron相关
### 访问外部接口，跨域问题
直接在`new BrowserWindow`的配置里边增加一句`webPreferences: {webSecurity: false}`
来自：[segmentfault](https://segmentfault.com/a/1190000012030202)
