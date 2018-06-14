# leaflet相关
### 创建新组件，设置自定义options不起作用
要使用`L.setOptions(this, options);`来设置options，如果通过`L.Util.extend(this.options, options);`设置则会把原型中的options改变，使得整个组件都会是这个设置。
PS：当然，如果如果当前只有一次组件，看不出来影响。
