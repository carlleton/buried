# vue功能相关
## axios实现文件下载
```js
// Here is a hack, works well for me.
// You can put it into `transformResponse`, etc as well.
import fileDownload from 'js-file-download'

opts.responseType = 'blob' // <--- force blob at the beginning, anyway

res = await axios(opts)

let resBlob = res.data // <--- store the blob if it is
let resData = null

try {
  let resText = await new Promise((resolve, reject) => {
    let reader = new FileReader()
    reader.addEventListener('abort', reject)
    reader.addEventListener('error', reject)
    reader.addEventListener('loadend', () => {
      resolve(reader.result)
    })
    reader.readAsText(resBlob)
  })
  resData = JSON.parse(resText) // <--- try to parse as json evantually
} catch (err) {
  // ignore
}

// Now you have `resData` and `resBlob` at the same time.
// `resData` would be the normal data object,
// or the error object if `resBlob` is expected.

if (resData) {
  if (resData.error) {
    // handle error
  } else {
    // handle data
  }
} else {
  // handle blob
  fileDownload(resBlob, filename)
}
```
来自：https://github.com/axios/axios/issues/815#issuecomment-340972365


```js
// ops 为用户配置
let res = await axios({
  ...opts,
  // 这里通过 blob 接受传输流
  responseType: 'blob'
})

let resBlob = res.data
let resData = null
try {
  let resText = await new Promise((resolve, reject) => {
    // 通过 FileReader 接受并解析
    let reader = new FileReader()
    reader.addEventListener('abort', reject)
    reader.addEventListener('error', reject)
    reader.addEventListener('loadend', () => {
      resolve(reader.result)
    })
    // 文件
    reader.readAsText(resBlob)
  })
  // JSON
  resData = JSON.parse(resText)
} catch (err) {
}
return { res, resData, resBlob }
```
我们可以将上述部分封装为一个方法，每次请求时调用上述方法即可。
```js
download(data) {
  // 将上述部分导出为 $ajax 并在使用时导入
  return $ajax({ method: 'GET', url: 'download', data })
}
```

作者：Geovanni.zhang
链接：https://www.zhihu.com/question/263323250/answer/267842980
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
