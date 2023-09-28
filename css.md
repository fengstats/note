# CSS

## 基础 | basis

### 层叠样式表 | cascading style sheet

- 内联样式（inline style）
- 内部样式（internal style sheet）
- 外部样式（external style sheet）
- 通过 "@import" 导入（在 .css 文件中写）

进制

- 0b：二进制
- 0o：八进制
- 0x：十六进制

RGB：色彩空间（红绿蓝三原色），通过调整这三种颜色的不同比例，组成其他的颜色

- RGB 取值比例为 0-255，也就是一个颜色可以取 256 种，共计 1678 万种颜色可能
- rgba(0, 0, 0, 0.9)：a 为 alpha，可选，在此表示透明度，0-1 之间的数值或者百分比

**浏览器的网页渲染流程：**

1. load html：加载 html 文件
2. parse html：解析 html 文件
   1. load css：加载 css 文件
   2. parse css：处理 css 文件
   3. 需要注意的是在这里的 css 加载并不会阻塞 html 向下执行，而是异步（async）加载，等到解析完成之后呢再将 css 样式附加（attach）html dom tree 上，生成 render tree（浏览器最终想要的东西）
3. create dom tree：创建 dom 树
4. display：在网页中显示

text-transform：转换单词大小写（从来没用过…）

- capitalize：首字母大写
- uppercase：全部大写
- lowercase：全部小写
- none：无

text-indent：用于设置首行缩进，单位可以写 px/em，em 是相对于字体大小的倍数设置的

**text-align**

文本对齐方式（mdn 直译）

还有 text-align-last：最后一个，text-align-all：所有

- left/right/center：左/右/中心
- justify：两端对齐
- 这个属性其实不至可以用于文本，还能用于其他的元素对齐（所有行内元素），所以 mdn 的取名/解释有歧义

font：字体

- size：大小
- family：字体族名
- style：风格（normal/italic）
- variant：变形，设置 small-caps 可以将小写字母替换为缩小版的大写字母
- 缩写：
  1. style, variant 和 weight 可以不写，可以随意调换位置
  2. size 和 family 必须写，且要保持次序
  3. font-size/line-height，line-height 可以不写，但是如果写必须跟着 font-size 后面（/）

line-height：文本行高（一行文本所占据的高度）

1. 严格定义：两行文本基线（baseline）之间的距离
2. 一行文本中存在：顶线（top）、中线（middle）、基线（baseline）、底线（bottom）、行距
3. line-height 直接写数值不跟单位时，代表相对于 font-size 的倍数，如 1.5、2 的等等

**选择器（selector）**

1. 通用选择器：`*{}`
2. 简单选择器：元素（h1/p/img）、类（class）、id
3. 属性选择器：`[]{}`，比如 `<div title="a">文本</div>` 要选中，用 `[title]{}` 或者 `[title=a]{}` 即可
4. 后代选择器：多个选择器连接使用空格（space）隔开，直接子代使用 `>`（大于号）
5. 兄弟选择器：`+` 表示选择相邻的最近的一个兄弟元素，`~` 则是选择同级内所有兄弟元素
6. 选择器组
   1. 交集选择器：同时符合两个选择器条件的，如 `div.box{}` 就是选择既是 div 元素同时又拥有类名为 box 的 HTML 元素
   2. 并集选择器：满足众多选择器中的一个条件即可，以 `,` 分隔，一般用于给多个元素设置同样的样式

**伪类（Pseudo classes）**

动态伪类：以一个 `:` 开头，需要按照顺序，否则可能不生效（LVFHA）

1. :link：未访问
2. :visited：已访问
3. :focus：聚焦
4. :hover：悬停
5. :active：点击

结构伪类

1. :nth-child(n)：n 为自然数，0 和任意整数，这里其实是一个变量的存在

- n：选中所有
- n=1：选择第一个
- n=2n：选择偶数
- n=2n-1/2n+1：选择奇数
- -n+2：选择前两个

2. :nth-last-child(n)：从后往前找
3. ntf-of-type(n)：查找时排查干扰项，只选择于目标选择器相同类型的

**伪元素**

可以使用 `:` 开头，也可以 `::` 开头，但是为了和伪类区分开，我们一般使用两个 `::`

1. ::first-line：选中首行
2. ::first-letter：选中首字母
3. ::before：在元素前
4. ::after：在元素后

**CSS 的继承性（inherited）**

1. 如果一个属性拥有继承性，那么在该属性设置之后，其后代元素都可以继承这个属性的值为默认值，若后代元素自己已经设置了这个属性，当然是以自身为第一有优先级
2. 想知道哪些属性拥有继承性的话，多写多试，或者多看 MDN 文档，一般都有详细说明
3. 如果一个属性没有继承性但是我想要它继承父元素或者祖先元素的这个属性对应的值，此时怎么办？可以给这个属性设置一个 `inherit` 的值，这样就强制让它拥有了继承性

CSS 的层叠（Cascading）

**CSS 翻译过来就是层叠，那么到底什么是层叠呢？**

1. 一个元素，我们可以通过不同的选择器来给它设置同个属性中不同的值，但是最终浏览器只会呈现一种效果
2. 这是因为属性的效果会被浏览器一层一层的覆盖上去（可以看成一个三维平面 x/y/z）
3. 最终的效果生效要看我们的选择权重，权重一样时看先后，后来者居上（权重可以叠加）
4. 权重顺序：!important > 内联样式 > id > 类/属性/伪类 > 元素/伪元素 > 通配符

**HTML 的元素类型**

1. 块级元素（block）：元素非常重要，独占一行显示，可以设置宽高属性（特性）
2. 行内级元素（inline）：一般表示元素不是那么重要，可以和其他行内级元素一起显示在一行中（特性）
3. 行内块级元素（inline-block）：同时拥有块级元素和行内级元素的特性
4. 行内替换元素（inline-replaced）：这个值不能通过我们手动来设置，只是一些特别的标签/元素会有，比如 img/iframe/video/input，他们的特点就是展现效果并不是由 CSS 来控制的，简单来说，他们的内容不受到当前文档的样式影响，可以和其他的行内级元素在同一行显示，也可以设置宽高特殊：不要在 p 标签内当 div 标签，否则渲染显示会出问题（div 这里代指所有块级元素，意思就是行内级元素内最好不要去放块级元素）

HTML 中隐藏元素的几种方式

1. display: none;（元素不显示，且不会占据空间）
2. visibility: hidden;（元素不可见，但是会占据空间）
3. 颜色方案（不可见，占据空间）
   1. color: rgba(0, 0, 0, 0); Alpha 为 0，代表透明，不过选中可见，不会影响到子元素
   2. background-color: transparent; 背景透明，不影响前景显示
   3. opacity：整体元素完全透明，包括子元素

**CSS 中的盒子模型（Box Model）**

1. content：内容
2. padding：内边距（设置百分比是相对于包含块/父元素宽度的，要慎用）
3. margin：外边距（设置百分比是相对于包含块/父元素宽度的，要慎用）
4. border：边框

行内元素的边距问题

1. 上下 margin 无效，左右 margin 会生效
2. 上下 padding 从显示的效果上来看是增加的，但是不会影响周围的其他元素布局，所以是无效的，左右 padding 会生效

上下 margin 的传递（一般是父子之间，对了，左右 margin 是不会传递的）

1. 上 margin 触发条件：如果当前块级元素的顶部线条和父元素的顶部线条重叠，则当前元素的 margin-top 值会被传递给父元素，导致浏览器呈现效果于自己想象有出入
2. 下 margin 触发条件：父元素高度设置为 auto，其余与条件触发与上 margin 基本相同，主要是底部线条重叠
3. 如何防止？
   1. 把 margin 换成 padding
   2. 给父元素设置一个 border 为 1px 的边框
   3. 设置 overflow: auto;（开启 BFC 模式，相当于给父元素一个独立的空间，这样就不会影响了）

上下 margin 的折叠（collapse）

- 比如两个紧挨着的兄弟块级元素
- 上面的设置了 margin-bottom: 50px;
- 下面的设置了 margin-top: 100px;
- 最后只会显示一个，那就是两值相比，取最大，也就是 100px
- 其实感觉也没啥问题，因为上面元素要得 50px 我已经达到了，所以说并不是没有生效，而是下 jj 面设置的值比你更大，把你的值效果涵盖掉了，还有人说为什么不是从上面的 margin-bottom: 50px 之后的位置来设置 margin-top: 100px 的，因为本身元素之间的间距，就是和元素相关，并不是和你元素的间距所挂钩，是有个基准参考物的，我认为这个是没问题的

outline：外轮廓是不占据空间的（另一个标准流）

box-sizing：如何计算一个元素的总高度和总宽度

- content-box：默认值，元素的总高度/宽度计算不包含 padding and border
- border-box：元素的总高度/宽度计算包含了 padding and border
- 目前比较新的 Web 站点推荐使用 border-box 来重新更改盒子模型设置，能避免在布局内容时可能遇到的许多陷阱，IE8 早期的盒子模型用的就是 border-box

white-space 补充

- pre：不换行，空白处理不合并
- pre-wrap：换行，空白处理不合并
- pre-line：换行，空白处理合并

单行内容超出后显示省略号

```css
 {
  /* 不换行 */
  white-space: nowrap;
  /* 超出后隐藏 */
  overflow: hidden;
  /* 超出的文字替换为省略号 */
  text-overflow: ellipsis;
}
```

多行内容超出后显示省略号

```css
 {
  /* 超出后隐藏 */
  overflow: hidden;
  /* 超出的文字替换为省略号 */
  text-overflow: ellipsis;
  /* --webkit- 是为了兼容性 */
  display: -webkit-box;
  /* 设置显示几行 */
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
```

解决 img 标签引入图片失败问题（对付设置了限制的，而不是本身图片资源就有问题的）

```html
<img referrerpolicy="no-referrer" />
```

background-image 是可以设置多张图片的，`,` 逗号隔开即可，设置的第一张显示在最上面，其他图片按照顺序层叠于下方

background-attachment：决定背景图的位置是在视口内固定还是让它伴随内容区块滚动

- scroll：默认值，不滚
- local：滚

表格

单元格合并

1. 跨列合并：使用 colspan 属性，在想要合并的最左侧单元格写上 `colspan='合并几列就写几'`，并省略掉合并的 td 标签
2. 跨行合并：使用 rowspan 属性，在想要合并的最上面单元格写上 `rowspan='合并几行就写几'`，并省略下面多余的 td

input 中的 autofocus 属性可以实现自动聚焦

CSS 补充选择器部分

:only-child {}：如果只有一个子元素则选中

:root {}：根元素，相当于最顶层的 html 元素，全局的一些样式可以在这里写

:empty {}：元素内容为空时选择

:not(x)：否定伪类，满足 x 条件不选中，其余全部选中

Web Fonts（网络字体）

字体图标的好处？

- 放大后不会失真
- 任意切换颜色样式
- 有多个图标需要使用的时候，文件相对于图片要更小

CSS Sprite（精灵图/雪碧图）

是一种 CSS 的图像合成技术，将各种小图片合成到一张大图片上，然后使用我们 CSS 的背景定位和显示大小部分来控制想要显示的对应小图片

好处？

1. 减少了图片资源总数量
2. 减少了 http 的请求数量，减轻了服务器压力，提高了网页的响应速度
3. 解决图片的命名困扰（PS：感觉对我来说没有，因为使用的时候我们还是要给 class 取设置名称的）

cursor 的显示效果

- auto：根据浏览器上下文决定显示效果
- default：根据你的操作系统决定
- point：一只小手
- text：一根竖线
- none：无表现

解决多个行内级元素中间在浏览器中显示中间会多一个空格的问题

1. 直接删掉源代码中的换行
2. 父元素设置 `font-size: 0` 子元素再设置回正常值
3. 通过 float 调整为一个方向
4. 设置 `display: flex` 自动清除

CSS 中的几种居中方案

- 水平居中（前提是当前元素拥有固定宽度）
  1. 行内块级元素：在其父元素上设置 `text-align: center`
  2. 块级元素：设置 `margin: 0 auto;`
  3. 定位：给父元素设置相对定位，给当前元素设置绝对定位，`left: 0; right: 0; margin: 0 auto;`
  4. flex：父元素设置 flex 布局并设置属性：`justify-content: center;`
  5. flex：父元素设置 flex 布局，子元素设置 `margin: 0 auto;`
  6. . 通过定位（替换 margin）+ transform（可以参考垂直居中）
  7. 通过 margin 配合 transform 中的 translateX `margin-left: 50%; transform: translateX(-50%);`，

补充：margin percetage 方案不能适用与垂直居中，因为其 percentage 值是相对于包含块的 width 来计算的

- 垂直居中（前提是当前元素拥有固定高度）
  1. flex：父元素设置 flex 布局，`align-items: center;`
  2. flex：父元素设置 flex 布局，子元素设置 `margin: auto 0;`
  3. 定位：给父元素设置相对定位，给当前元素设置绝对定位，`top: 0; bottom: 0; margin: auto 0;`
  4. 定位 + transform：`top: 50%; transform: translateY(-50%);`

### BFC（block formatting context）

- 在 BFC 中，box 会在垂直方向上一个挨着一个进行排布
- 垂直方向的间距由 margin 属性来决定
- 在同一个 BFC 中，两个相邻 box 之间垂直方向的 margin 会被折叠（collaspe）
- 在 BFC 中，每个元素的左边缘是紧挨着包含块（containning block）的左边缘的

哪些情况会形成一个新的 BFC？

- [Block Formatting Context](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

BFC 的作用？

- 解决 margin 上下折叠：通过形成一个新的 BFC 作用域，在其内部设置 margin 属性值
- 解决 float 高度塌陷：给浮动元素的包含块设置 BFC，此时整个包含块会增加高度至能包括所有浮动元素的下边缘，以此来达到解决浮动的目的，并不是让浮动元素给包含块汇报高度，同时此方案对绝对元素无效

### 媒体查询

## 定位

### 标准流 | static

定位的默认值，表示静态定位，在网页中从左往右，从上到下按照顺序排好，不会出现层叠现象这种就是标准流

如何对标准流进行定位呢？

通过 margin、padding 进行调整，但是会有两个缺点

1. 通常会影响标准流中其他元素的显示效果
2. 不便于我们实现层叠关系

### 相对定位 | relative

1. 会相对于自己本身的位置进行定位/移动
2. 特点
   1. 原先的位置会被占用，其他标准流元素无法正常使用（所以是不脱标定位）
   2. 定位到其他位置时不会影响元素布局
3. 使用百分比进行定位的时候是相对于父元素

### 固定定位 | fixed

1. 相对于视口（viewport）进行定位/移动
2. 特点
   1. 不占位置
   2. 脱标元素（脱离标准流）

### 绝对定位 | absolute

1. 相对于离它最近的一个祖先定位元素（非 `static` 的），没有则相对于视口/初始包含块 ICB（initial containing block）
2. 特点
   1. 不占位置
   2. 脱标
3. 通常我们用的比较多搭配方案的就是子绝父相，当然也可以子绝父绝或者子绝父固

### 粘性定位 | sticky

这是个新属性，如果是低版本浏览器开发者需要先考虑兼容问题

1. 可以把它看作相对定位（relative）与固定定位（fixed）的结合体
2. sticky 是相对于最近的滚动祖先元素视口来定位的（the nearest ancestor scrool container scrollport）
3. 举个例子：
   ```css
   #one {
     position: sticky;
     top: 10px;
   }
   ```
   - 在视口滚动到元素 top 距离小于 10px 之前，元素为相对定位
   - 小于 10px 之后，元素为固定定位
   - 直到重新回到此阈值以下

### z-index

1. 只能作用在定位元素上，其他元素无效果
2. 比较原则
   1. 兄弟元素：z-index 越大，层叠等级就越高，显示就越靠前
   2. 不是兄弟元素：找祖先层级一致的定位元素比，找不到就比不了

### 一些小小的补充

**将元素设置为 absolute/fixed 之后，元素会产生以下特性：**

1. 不再受到标准文档流的约束（脱标）
2. 可以随意设置宽高（既是原先是行内级元素）
3. 宽高默认由内容撑开
4. 不会再给父元素上报宽高信息（比如父元素本身未设置宽高的情况下，整体的宽高都是由当前的定位元素撑起来的，那么当这个元素脱标的那一刻，宽高数据将不再属于父元素）
5. 内部的子元素依旧按照标准文档流进行布局

**对于绝对定位元素的宽高计算公式**

1. 定位参照对象（你当前定位元素所相对的一个父级或者祖先级元素，有可能也是定位元素）的宽度： `left + right + margin-left + margin-right + 元素实际占用的宽度`
2. 定位参照对象的高度 `top + bottom + margin-top + margin-bottom + 元素实际占用的高度`

TIP：假设当前的元素的父元素是相对定位，你想要实现居中

```css
 {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  /* 想要通过绝对定位来实现水平垂直居中需要子元素设置宽度与高度 */
  /* 否则的话因为默认的 width/height 是 auto, 会把父元素占满 */
  width: 80px;
  height: 80px;
}
```

## 浮动

历史：浮动最初只是单纯的用于在文本内的浮动图像或者说实现图文环绕的效果，但是早期的 CSS 标准中并没有提供较好的布局方案，因此导致在一段时期，浮动成为了多列布局中最常用的工具

特性：

1. 脱标元素，但是左/右边界不会超过包含块（containing block）
2. 浮动元素之间不能层叠
3. 浮动元素不能和行内级元素层叠，行内级元素会被推出来（图文环绕的原理）
4. 元素对齐方式为顶部对齐

### 浮动产生的问题

高度塌陷：由于浮动元素会脱标，所以在父元素无固定高度需要内部子元素来填充高度时就会发生高度塌陷问题

怎么解决？

1. 在所有浮动元素之后添加一个块级元素，并设置其 CSS 样式 `clear: both;`
2. 手动添加 html 元素的方式不太优雅，我们也可以使用我们 CSS 的伪元素形式来完成，但需要注意的是伪元素本身是属于行内级元素，不要忘记给它重新设置类型等级

```css
.clear-fix::after {
  content: '';
  clear: both;
  display: block;
  /* 兼容低版本浏览器写法 */
  visibility: hidden;
  height: 0;
}

.clear-fix {
  /*  兼容IE6/7 */
  *zoom: 1;
}
```

## flex | Flexbox

这是一种比较新的布局方案（一维布局，grid 是二维布局方案），可以按列或者按行来布局元素，学完 flex 基本上你在网页中所看到的布局都可以实现出来

flex 父容器：flex container

flex 布局的子元素：flex-items

轴的方向开始点：flex-start

轴的方向结束点：flex-end

### 主轴 | main axis

默认从左到右，flex-items 会沿着这个轴所排列，可以通过 flex-direction 来改变主轴的所属

### 交叉轴 | cross axis

如名，和主轴交叉的轴就是交叉轴

### flex container 属性解析

flex-direction：row/row-reverse/column/column-reverse; 默认值为 row，用于设置主轴方向以及改变 flex-start/end 朝向

flex-wrap

- nowrap：默认值，不换行
- wrap：换行
- wrap-reverse：换行，且 cross axis 的 flex-start 方向与 flex-end 调换

flex-flow：direction 和 wrap 的简写属性，次序任意，但是至少要写一个

justify-content：常用的属性，用来调整 flex items 在 main axis 方向上的对齐方式

- flex-start：默认值，与 main axis 的 flex-start 一致
- flex-end：与 main axis 的 flex-end 一致
- center：flex items 居中对齐
- space-between：flex items 之间的间距相等，且两端对齐（首尾不留间隙）
- space-around：两端右间距，是正常 flex items 之间的一半
- space-evenly：这个属性比较新，可能会有兼容问题，与 space-between 不同的点就是两端也会右间距且这个间距就是 flex items 之间的间距

align-items：可以使用在 CSS 网格布局和 Flexbox 布局中，在 Flexbox 布局中是用来调整 flex items 在 cross axis 中的对齐方式

- normal：默认值，在 Flexbox 布局中与 stretch 效果一致
- stretch：当 flex-items 在 cross axis 的 size（看方向，如果没有修改 direction 的情况下，就是 height，修改为 column 之后就是 width）为 auto 是，会自动拉伸填充满 flex container
- center：居中对齐

align-content：在存在多行 flex items 时，调整 flex items 在 cross axis 中的对齐方式（参数属性建议直接参考 justify-content，你甚至可以把这个属性当成改变了 direction 后的 justify-content）

### flex items 属性解析

order：默认值为 0，决定了单个 flex item 的排布顺序，单位为任意任意整数（0/-n/+n），值越小层叠等级越高

align-self：默认值为 auto，用于设置单个 flex item 在 cross axis 中的对齐方式，优先级比 flex container 中的 align-items 高

flex-grow：默认值为 0，成长属性，给 flex item 拉伸/填充设置数值，单位为非负数字即可（当 flex container 在 main axis 方向上右剩余 size 时，才会生效）

flex-shrink：默认值为 1，收缩属性（flex container 在 main axis 有超过部分时才会生效）

flex-basis：默认值为 auto，基础尺寸，设置一个具体的值或者 content

flex: 缩写属性 flex-grow、flex-shrink、flex-basis

语法：`none | [<flex-grow> <flex-shrink>? || <flex-basis>]`

`|`：只能选一个

`[]`：组合成整体，用于强调优先级

`||`：或组合符，不过至少要出现一个

`？`：0 或 1，代表这个参数可以省略

## transform

平移：translate(x, y)

缩放：scale(xy) / scale(x, y)

旋转：rotate(deg)

倾斜：skew(xdeg, ydeg)

补充：可以通过 transform-origin 来改变原点坐标位置，这样在我们对元素进行形变时就可以更自由的控制

## transition

动画作用属性：transition-property

动画持续时间：transition-duration

动画曲线效果：transition-timing-function

- linear：线性的，均匀动画
- ease-in：开始慢，后面快
- ease-out：开始快，后面慢
- ease-in-out：开始和后面慢，中间快画延迟时间：transition-delay

## CSS animation

对比 transition 的好处就是，可以逐帧设置自己想要的动画，解决了 transition 只有两帧动画可以设置（首尾）动画执行的过程中无法控制，自定义程度更高了，可以执行多次动画，也可以对动画进行控制（暂停/继续）

```css
@keyframes animationName {
  0% {
  }
  50% {
  }
  100% {
  }
}

.box {
  animation: animationName linear 2s;
}
```
