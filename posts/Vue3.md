Vue3 关于 watch 监听异常的问题：[Vue SFC Playground](https://play.vuejs.org/#eNp9Ustu2zAQ/JUtL3IAV0bqmysbfaVAe2iNpuiJF0ZeWUookiAp24Cgf++StGWljxz82J3Z4Sw5PXtvTH7okK1Y4UrbGA8OfWc2XDWt0dZDDxYrGKCyuoWMqNkIfdStOffzRSiCUvaWq1IrF4SELevP2rafhBewDkKzniuAHdVOd7bEFWTZnKvh5jLUuPtaH8/kSkiHI1TKpnwiZHYD603USeT8IGSHBLya1iTKVbFIS9E6VHhsjRQeqer75+4GIgMUD533WsG7eNSas/jL2ebBk1QCaZiIcfWVsdq4rbCidUTu8zz/Q5VGi3gzacrA4XVTETUZJfT2zbJYBLRYjO7YnHlHK1fNPn90WtHbxG3JDik1Eu134xu6Es5WEJGACSn18WvsedshXWrqlzWWT//oP7pT6HG2tejQHpCzEfPC7tEn+O7+G57o/wi2etdJYr8A/kCnZRc8JtqHTu3I9oQX3X6JMWrU/qe7O3lU7rJUMBqYQ+RzRrEKl/i/1a92l/kyztHj0y1eIvl3uO0k3kfhy/p5wAkOnxS7+MiUrh1WjcJtqCjFBNPZkwCQnyF0Kcr0HUVnMamJlE+oc5hRROeg5e6XkJFzEYRwppaYS72fZVElmwOxo2rSvob67HMS7KhS1Lebvp+ag2EoFtRN49ekDb8BKb5eEQ==)

17:35 因为父组件内的 template 中使用了 isShow 用于控制显示/隐藏，每次更新 isShow 的值都会重新渲染一次 template，且你在进行子组件的 props 传值的时候使用的是 `…`（解构赋值），意味着每次传入子组件内的 propsParams 都是不一样的，自然会触发 watch 监听

- 验证：要么把使用 isShow 变量的 `<p>` 去掉
- 解决：改成 `:propsParams="searchFormData"`

Vue3 使用 ref 包裹数组，通过 list.value.push 的方式，设置 watchEffect 打印 list.value 不能更新，但是 Vue SCF Playground 可以

- [watchEffect not triggering properly with reactive or ref objects · vuejs/core · Discussion #9428 · GitHub](https://github.com/vuejs/core/discussions/9428)

问题：SCF 劫持了 console.log [repl/src/output/srcdoc.html at main · vuejs/repl · GitHub](https://github.com/vuejs/repl/blob/main/src/output/srcdoc.html#L159-L172)
解决：[Vue SFC Playground](https://repl-vuejs.vercel.app/#eNp9Uk1v1DAQ/SuWL81KK5cVnMruCqj2AAdAgMQBc0idSeLWsS1/bBZF+e+M7e02laoeEtlv3jy9eeOJfrSWHSPQG7r1wkkbiIcQ7Z5rOVjjApmIg3ZNxjqI/tC2IAKZSevMQDjFRk7fcy2M9oEoib9dold//q4usFBSPGw2WKlWZLcnE9ckc9mxVhGYjb6vNpvUMONXtVGLII1O9MwtMrJ19QCo0hgRB9CBCQd1gIOCdKuuCuFqlVrKmY2yCT22vFlgPciuTz4zeBG7M80/VlsLurntpWqqQs9qo9SNGVnyYVSycJZCIGDv72dlnKJaYdsisGox+JnFlOmqpxDy8Om3vS5bwPzxEmCwCmfEGyHbuxgCxvIhB7rj9Bwsp/t82l4XQiZPU1nHPCfNhQ5d0+DRRCs7du+NxsVnXyhnBisVuG82pe85vSmOU61WyoxfMhZchPUjLnoQDy/g9/6UME6/O/DgjvhMLrVQuw5CKR9+foUTni/FwTQRM3yt+AMwwJg8FtqnqBu0veBlt5/z85W6++UPJ1yTfxwqGU3MOfPzI759ZfQnu2/Zu9yHq6LzfzIkFzk=)
