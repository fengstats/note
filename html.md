## HTML

img 是一个可替换元素（replaced element)

a：锚元素（anchor）

- href：超文本引用（hypertext reference）
  - 如何实现使用 a 标签来跳转网页具体位置（attr 可自定义）
    1. 需要跳转到位置的元素上写上 `id="attr"`
    2. 设置 `href="#attr"` 即可
- target：目标
  - \_self：默认值，当前页面打开
  - \_blank：空白页打开，新页面
  - \_parent：父窗口打开
  - \_top：顶层窗口打开

iframe：内嵌网页元素

- src：目标网页地址（部分网页会有监测机制拦截 iframe 的内嵌）
  - 一般是通过设置 Headers -> Response Headers -> "X-Frame-Options" -> SAMEORIGIN
  - 可以通过 nginx
- frameborder：是否显示边框，1 显示，0 不显示

URL 和 URI 的区别

- URI：统一资源标识符，标识 Web 技术使用的逻辑或物理资源
- URL：统一资源定位符，俗称网络地址，相当于网络中的门牌号
- 总结：URI 包含了 URL（子集概念），但是 URI 不一定是 URL

常用的全局属性（id/title/class/style）

SEO：搜索引擎优化（search engine optimization）

- SEO 就是通过了解搜索引擎的运作规则来调整我们的网站，提高网站排名的这个过程
- 比如我们的元素语义化，网站内的关键词与网站本身所做的事符合程度，能够让搜索引擎爬虫更好的收录网站信息

元素语义化：用正确的标签/元素去做正确的事情

有什么好处？

1. 方便我们代码的维护
2. 减少开发的沟通成本（不同的元素在被 W3C 所制定的时候就已经存在意义了，比如我们看到代码中写了 h 标签，那么我们第一反应这个就是个标题，是比较重要的元素，又或者看到 img 标签，那我们就知道这里要放一张图片）
3. SEO 优化
4. 能够让浏览器中的语音工具更好地识别我们的元素用途

unicode 是为了解决大部分中文编码问题而生的
