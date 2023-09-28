什么是语义化版本控制？

- [语义化版本 2.0.0 | Semantic Versioning](https://semver.org/lang/zh-CN/)

随意在站点上动态的渲染任意的 HTML 可能会非常危险，因为会很容易导致 XSS 攻击，建议只对可信内容使用 HTML 插值，绝对不要将用户提供的内容作为插值

对于布尔类型的 attribute v-bind 工作起来会略有不同（有值意味着 `true`），在下面的例子中，如果 `isButtonDisabled` 值为 `null`、`undefined` 或 `false` 的时候，该 attribute 甚至不会被渲染到 `<button>` 元素中

```html
<button v-bind:disabled="isButtonDisabled">Button</button>
```

动态参数会存在一些约束（Vue2.6+ 特性），如下

- 对于动态参数值：预期要求一个字符串，异常情况下为 `null`，这个特殊的值可以用于显性的移除绑定，任何其它非字符串类型的值将会触发一个警告
- 对于动态参数表达式：有一些语法约束，如空格和引号（因为放在 HTML attribute 中是无效的），将会触发编译警告，可以通过使用没有空格或引号的表达式（例如将复杂的表达式通过计算属性来替代
- 对于动态参数表达式：在 DOM 中使用模板时（直接在 HTML 文件中写），需要避免使用大写字符来命名键名，因为浏览器会将 attribute 名强制转换为小写，若你的实例中对应的 property 是大写，那这可能会导致代码无法正常工作
