# 基础部分
### input file重复选择文件时不能判断
有时用户上传相同附件时也需要触发input[type='file']的change事件，除了将form重置外，还可以将input的value设为空
```html
<input type="file" id="test" name="test" multiple>
```
```js
var fileinput = document.getElementById('test');
fileinput.onchange = function() {
    if (this.value) {
        console.log(this.value);
        //重置，IE11会触发change事件
        this.value = '';
        //IE9,IE10需要重置type
        this.type = 'text'
        this.type = 'file'
    } else {
        //value设为''触发的change（IE11）
        console.log("已重置")
    }
}
```
来自：http://www.cnblogs.com/zoex/p/reset-file-input.html

### 使用LESS时calc，请使用`~`来计算。其他语言转为LESS时也需要专门注意
`calc(~"100% - 120px");`

### HTML5中input框type=number中取值问题
当输入不是数字时，Chrome获取值为空，可判断`.validity.badInput`为true提示非法数值，Firefox和IE都能取到非数字的字符串
来自：https://blog.csdn.net/yzj_work/article/details/26756015

### 正则表达式使用new Reg()，如果涉及中文会转换
`let reg = new Reg("[\u4E00-\u9FA5]+")`和`let reg = /[\u4E00-\u9FA5]+/`，这两个`reg.test('中')`识别效果不一致，因为new Reg("")会将编码转换
