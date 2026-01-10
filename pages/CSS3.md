- 什么是CSS？CSS 能够做什么？
  collapsed:: true
	- CSS，即层叠样式表，是 HTML 页面的表现层。
	- CSS 能做什么？
	  collapsed:: true
		- 布局控制（元素位置、盒模型、浮动等）
		- 样式化HTML元素（字体、颜色、大小、背景等）
		- 字体和排版控制（文字字体、大小、行高、字间距等）
		- 响应式设计（媒体查询）
		- 用户交互响应（伪类、伪元素），为鼠标悬停、点击、焦点等状态定义不同样式
		- 动画和过渡效果（关键帧动画、过渡属性以及动画属性）
	- CSS 三大特征
	  collapsed:: true
		- 层叠性
		  多个**样式规则**可以同时作用于**同一个元素**。样式规则可能来着不同源（开发者样式、用户样式、浏览器内置样式），浏览器按照一定**优先级**对样式进行叠加，高权重规则会**覆盖**低权重规则（形成了一个层级关系），层叠概念因此而来。
		  开发者样式包括：内联样式（style 属性）、嵌入式样式（style 标签包裹）、外联样式（link 标签引入）
		- 继承性
		  浏览器允许子元素的**部分属性**没有设置**相当的属性**时，会默认从**父元素**中继承，并非所有样式属性都具有继承性。
		- 优先级
		  值得是 CSS 选择器的优先级，由选择器类型和数量共同决定
	- 继承性
	  collapsed:: true
		- ![CSS可继承属性.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/57edb254cdaf44e68fcc4ab2b4d3abe7~tplv-k3u1fbpfcp-jj-mark:1512:0:0:0:q75.awebp#?w=2104&h=1664&s=341104&e=png&b=fffdfd)
		- ![CSS不可继承属性.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3d8f78098fdc4e9a897b0f21d488bea5~tplv-k3u1fbpfcp-jj-mark:1512:0:0:0:q75.awebp#?w=2264&h=3160&s=675856&e=png&b=fffcfc)
	- 理解四个常见属性值
	  collapsed:: true
		- ~~`default` 表示属性默认值，通常指浏览器内置样式表（user agent stylesheet）中为特定元素和属性定义的默认值。~~。`default`是 CSS 中的保留字，不是一个有效的属性值。
		- `inherit` 表示属性将继承其父元素的值。
		- `initail` 表示该属性将被重置为*该属性在 CSS 规范中的初始值*，可作用于任意 CSS 属性。
		- `unset` 表示属性将被重置为其关联的样式值。如果该属性默认为**继承属性**，则该值等同于`inherit`，如果该属性为**非继承属性**，则该值等同于`initial`。
		- `revert` 表示将属性值重置为*浏览器默认样式*或*用户代理样式*。
- BFC
  collapsed:: true
	- BFC 是 CSS 中的一种布局上下文，影响了元素在文档中的布局和渲染方式。
	  BFC 是一个独立的渲染区域，其中包含了一组块级盒子。
	  设置了 BFC 的元素，会形成一个**独立的布局环境**，其内部的元素按一定的规则来布局定位，不会收到外部元素的影响，同时也不会对其他外部元素产生影响。
	- BFC 能够产出的效果
	  collapsed:: true
		- **消除边距折叠**，两个元素在**同一个 BFC**内，才会发生垂直外边距的折叠（嵌套元素、相邻元素）。
		- **清除浮动**，BFC 区域不会和**浮动元素**发生重叠，因此能够解决父元素高度塌陷的问题。
		- **自适应两栏布局**，原理同上，右侧栏形成独立的BFC，不会与 float 元素重叠。
	- 触发 BFC 条件
	  collapsed:: true
		- 根元素（html 元素）
		- float属性为 left 或 right
		- position 属性为 absolute 或 fixed
		- display 属性为 inline-block、flex、inline-flex、grid、inline-grid、table、table-cell
		- overflow 属性为非 visible 的值（auto、hidden、scroll）
- 选择器 & 优先级
  collapsed:: true
	- 优先级
	  collapsed:: true
	  用于确定多个 CSS 规则作用于同一元素时，那个规则被应用。
		- id:: 68a927a5-fa14-4314-9208-c57bd06e7ab6
		  | 选择器      | 优先级 | 备注     |
		  | :---        |    :----:   |          ---: |
		  | 内联样式      | 1000       | html 中的`style`属性   |
		  | ID 选择器   | 100        | `#id`语法选择的元素      |
		  | 类、属性、伪类选择器 | 10       | `.class`、`[type="text"]`、`:hover`      |
		  | 标签、伪元素选择器   | 1        | `div`、`::before`、`::after`     |
		  | 兄弟、相邻兄弟、子元素、后代、通配符选择器| 0        |  `div ~ p`、`div + p`、`div > p`、`div p`、`*`    |
		- 具有相同优先级的 CSS 规则，则**后定义**的优先级更高。
		-
		- 特殊关键字
		  collapsed:: true
			- `!important`
				- 未使用 important 关键字时，优先级顺序：`开发者样式 > 用户样式 > 浏览器样式`
				- 使用 important 关键字时，优先级顺序：`浏览器样式 > 用户样式 > 开发者样式`
			- `@layer`
			  作用：将样式表分组
				- 语法规则：
				  ```css
				  /* 具名级联层，带有具体样式规则 @layer layer-name {rules} */
				  @layer base {
				      :root {
				          background-color: #f5f5f5;
				          color: #333;
				      }
				  }
				  @layer components {
				      button {
				          background-color: blue;
				          color: white;
				          border: 1px solid blue;
				          outline: none;
				      }
				      button:hover {
				          background-color: darkblue;
				          border: 1px solid darkblue;
				      }
				  }
				  /* 具名级联层 @layer layer-name; */
				  /* @layer layer-name, layer-name, layer-name; */
				  @layer utilities;
				  @layer forms, buttons, text;
				  /* @layer {rules} */
				  @layer {
				      .clearfix {
				          clear: both;
				      }
				  }
				  
				  /* 与@import一起使用 */
				  @import url('./base.css') layer(base);
				  ```
				- 优先级规则
				  未使用`!important`关键字时，**没有分层的样式**优先级最高，其他则**按照声明顺序**排序，最后声明的优先级最高。
				  优先级并不是以下面具体定义的先后顺序为标准，而是以声明的顺序为标准。如果没有提前声明，则会以定义的先后顺序为标准。
				  ```css
				  /* 这种情况下，third优先级最高 */
				  @layer base, components, utilities, third;
				  
				  @layer third {
				      /* ... */
				  }
				  
				  @layer base {
				      /* ... */
				  }
				  ```
				  使用`!important`关键字时，没有分层的样式优先级最低，其他则**按照声明顺序**排序。
			-
		- 总结
		  在每一层中又遵循着`内联 > ID > 类 > 标签`的规则
		  用户样式：一般是由用户安装在浏览器中的插件注入的样式
		  ![WX20231124-100429@2x.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bb513bb7171b4c89ba7da3cdcc1fa630~tplv-k3u1fbpfcp-jj-mark:1512:0:0:0:q75.awebp#?w=1426&h=1310&s=196981&e=png&b=f6f1ef)
	- 选择器
		- 标签（元素）选择器，`p {}`
		- 类选择器，`.my-class {}`
		- ID 选择器，`#my-id {}`
		- 属性选择器，`input[type=text] {}`
		- 伪类选择器，`:hover {}`
		- 相邻兄弟选择器，`div + div {}`
		- 兄弟选择器，`div ~ div {}`
		-
	- `@规则（at-rules）`
	  collapsed:: true
	  用于在 CSS 声明一些特殊的指令或规则，通常在 CSS 文件顶部进行声明。
		- `@charset` 声明 CSS 文件的字符编码
		- `@import` 导入外部 CSS 文件
		- `@media` 定义媒体查询规则（根据不同的媒介类型、视口尺寸或设备属性）
		- `@font-face` 定义自定义字体
		- `@keyframes` 定义关键字动画
- 变量 & 函数
  collapsed:: true
	- 变量
	  collapsed:: true
		- 语法
		  ```css
		  :root {
		    /* css 变量以 --<变量名> 方式声明 */
		    /* 可以在选择器或全局作用域内定义 */
		    --primary-color: #1e90ff;
		  }
		  
		  .card {
		    --primary-color: #f17878;
		  }
		  
		  button {
		    /* 通过 var 函数对变量进行引用 */
		    background-color: var(--primary-color);
		    color: #ffffff;
		  }
		  ```
		- CSS 一键换肤原理
	- 函数
	  collapsed:: true
		- CSS 内部提供的标准函数
		  | 函数 | 说明 | 示例 |
		  | --- | --- | --- |
		  | `calc()` | 用于在样式中进行数值计算 | `width: calc(100% - 20px)` |
		  | `rgb()`、`rgba()` | RGB颜色值 | `color: rgb(255, 255, 255)` |
		  | `hsl()`、`hsla()` | 使用色相（Hue）、饱和度（Saturation）和亮度（Lightness）颜色值。色相取值范围是 0 到 360，饱和度和亮度取值范围是 0% 到 100%。 | `color: hsl(120, 100%, 50%)` |
		  | `url()` | 外部资源链接（背景图、字体等） | `background: url('image.png')` |
		  | `transform()` | 用于在元素上应用 2D 或 3D 变换操作（平移、缩放、旋转） | `transform: rotate(45deg)` |
		  | `linear-gradient()` | 创建背景渐变 | `background: linear-gradient(red, yellow)` |
		  | `repeat()` | 用于重复一个数值或一个指定的样式多次。它接收两个参数，第一个是重复次数，第二个是数值或样式。 | `grid-template-columns: repeat(3, 100px)` |
		  | `min()`、`max()` | 用于取一组参数中的最小或最大值作为最终的结果。它们可以在宽度、高度等属性中使用。 | `width: min(100%, 500px)` |
		  | `clamp()` | 用于限制一个值在一个指定的范围内。它接收三个参数，分别为最小值、推荐值和最大值。 | `font-size: clamp(16px, 4vw, 24px)` |
		  | `clamp()` | 用于限制一个值在一个指定的范围内。它接收三个参数，分别为最小值、推荐值和最大值。 | `font-size: clamp(16px, 4vw, 24px)` |
		  | `attr()` | 用于引用 HTML 元素的属性值，并将其应用于 CSS 样式中。它通常与 content 属性结合使用，用于在伪元素中插入元素的属性值。 | `content: attr(data-text);` 中，`data-text` 是元素的自定义属性 |
		  | `filter()` | 在元素上应用图像滤镜效果 | `filter: blur(5px)` |
- 盒模型及其特征
- 隐藏 & 显示
- 定位 & 浮动
- Flex 布局
  collapsed:: true
  弹性布局，即`display:flex`
	-
- 其他
	- 样式初始化
	  不同浏览器在标签默认样式存在不同，CSS 样式初始化能够避免不同浏览器间的样式差异
	  常用代码库`Normlize.css`
	- `link`和`@import`区别
		- 类型：link属于html元素，@import属于 css 语法规则
		- 加载时机：link标签在页面加载时就会被加载，@import引用则会等到页面加载完成后才会被加载