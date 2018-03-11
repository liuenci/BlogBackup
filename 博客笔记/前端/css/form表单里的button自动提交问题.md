做项目的时候写一个form表单，表单中有一个button按钮，这个按钮我以为默认的 type 就是 button,结果不是，默认不设置的时候，type=submit,就这和我项目出现的问题出现了答案，不显示设置 type = button ，只要点击这个按钮就会将整个表单提交到后台，所以解决方案就是以下语句。
```html
<button type="button">登录</button>
```
只有设置类型为 button 时才能保证点击这个按钮先执行自己写的脚本。
