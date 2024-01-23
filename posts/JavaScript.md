## 防抖和节流？

- 防抖：等待 N 秒后执行，若在 N 秒内再次触发，N 重新计时
- 节流：立即执行，但 N 秒内只会执行一次，若在 N 秒内再次触发，不处理

## 事件捕获和事件冒泡

- [冒泡和捕获](https://zh.javascript.info/bubbling-and-capturing)

## keyCode 废弃

- [告别 JS keyCode « 张鑫旭-鑫空间-鑫生活](https://www.zhangxinxu.com/wordpress/2021/01/js-keycode-deprecated/)
- [键盘键码值 KeyCode 参考，交互式获取 KeyCode - dute.org](https://www.dute.org/keycodes)

## for in 和 for of

for in 会将数组或者对象原型链上的属性也遍历出来，可以通过 hasOwnProperty 方法来只遍历自身属性

for of 只能遍历数组或者可迭代对象，必须要实现 iterator

## Object.keys 和 Object.values

Object.keys 也可以做到只遍历自身属性

直接通过对象插入新属性时，会通过对象 key 进行排序，所以在使用 Object.values 转换时 key 是升序返回的（只测试过 key 为 number 时）

## concat 和 ... 扩展运算符

小坑，concat 遇到多维数组合并时会自动展开一层内部元素，与扩展运算符 `...` 行为类似

`[[1,2]].concat([3,4])` 会变成 `[[1,2],3,4]`

## export 导出和 import 导入

你可以直接在需要导出的方法或变量前写 `export`

- `export const nickName = 'xxx'`
- `export function func() {}`

`export {}` 中的 `{}` 不是对象，只是导出引用的一种形式

⚠️ 这个导出和上面两个例子只能留一个，不要重复导出

- `export { nickName, func }`
- 通过 `as` 关键字：`export { nickNam as newNickName }` 设置别名，注意导入时需要导入别名。
- 默认导出 `export default xxx`，两者可以同时使用。

有导出就有导出 `import XXX, {} from 'filePath'` 前面的 `XXX` 是 `default` 导出，`{}` 内是 `export {}` 导出
