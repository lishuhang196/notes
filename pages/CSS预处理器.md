- 预处理器
  collapsed:: true
	- 主流CSS预处理器
		- `Sass`，在`CSS`基础之上，拓展了**变量**、**嵌套**、**混合**、**继承**等功能。
			- `Sass`语法风格为类似于`ruby`的缩进样式。
			- `Scss`语法风格类似于`CSS`的大括号样式。
		- `Less`，于原生`Css`风格类似，在此基础上也提供了**变量**、`嵌套`、`混合`等功能。
		- `Stylus`，使用缩进风格语法，不需要使用大括号和分号。
	- `PostCSS`，也具有预处理器的功能，但更像是一个工具集，通过插件系统，以拓展CSS的能力。、
	- 以上预处理器都提供（或部分提供）变量、嵌套、混合、继承、运算、条件判断、模块化等能力，可以帮助提高CSS代码的可维护性和重用性
- SASS
  collapsed:: true
	- 安装sass编译器
	  ```bash
	  npm install -g sass
	  sass --version
	  
	  // 编译 sass 文件
	  npx sass <input file> <output file>
	  ```
	- SCSS语法
	  collapsed:: true
		- 变量
			- 变量声明
			  ```scss
			  /*
			  声明一个scss变量
			  变量命名规则：
			  1. 使用小写字母，单词之间使用连接符（中划线或下划线）连接
			  2. 避免使用缩写或简写
			  3. 采用一致的命名规范
			  */
			  $cell-padding: 10px;
			  
			  // 变量使用
			  .item {
			    padding: $cell-padding * 1.5;
			  }
			  ```
			- 变量数据类型
			  ```scss
			  /* 数字类型，可为整数或浮点数 */
			  $font-size: 14px;
			  $opacity: 0.5;
			  /* 字符串类型，使用单引号或双引号标记 */
			  $font-family: 'Arial', sanas-serif;
			  $class-prefix: 'vant-';
			  /* 颜色，可为十六进制、RGB、RGBA、HSL或关键字 */
			  $body-color: #333333;
			  $primary-color: rgb(55, 120, 21);
			  /* 布尔值 */
			  $is-active: true;
			  $has-border: false;
			  /* 列表, 一组以逗号分割的值 */
			  $breakpoints: (640px, 768px, 1024px);
			  /* 映射，键值对集合 */
			  $colors: (
			  	"primary": #fff;
			    	"secondary": #0f0;
			    	"accent": #00f;
			  );
			  /* 空值，null */
			  $no-value: null;
			  ```
			- 变量插值，在`Sass`中使用`#{}`语法可将**变量值**嵌入到字符串中。
			  collapsed:: true
				- 基本插值
				  ```scss
				  /* 变量值可用于选择器、属性和字符串中 */
				  $prefix-class: 'vant';
				  $color: red;
				  
				  // 使用插值特性
				  .#{$prefix-class}-btn {
				    color: $color;
				  }
				  ```
				- 高级插值，变量插值可用于计算、函数和复杂表达式中，插值表达式中的计算结果可作为最终的值。
				  ```
				  $width: 100px;
				  .box {
				  	width: calc(#{$width} + 20px);
				      background: rgba(0, 0, 0, #{0.5})
				  }
				  ```
			- 作用域，Sass变量声明位置决定了其**可见范围**。
			  collapsed:: true
				- 局部作用域。默认情况下，变量在声明他的**规则块（选择器、函数）**范围内可见。
				  ```scss
				  .wrapper {
				    // 局部作用域
				    $primay-color: red;
				    .highlight {
				      // 在嵌套规则内访问变量
				      background-color: $primary-color;
				    }
				  }
				  
				  .btn-primary {
				    // 此处无法访问
				    // background-color: $primary-color;
				  }
				  ```
				- 全局作用域，在scss文件顶部声明的变量为全局作用域
				  ```scss
				  $primary-color: #ff0000;
				  
				  .btn-primary {
				      color: $primary-color;
				  }
				  
				  // 最好在顶部统一声明
				  $page-horizontal-padding: 20px;
				  $page-vertical-padding: 10px;
				  
				  .item-1 {
				    	// 在使用变量前，应先声明
				      width: $page-horizontal-padding;
				  }
				  ```
			- 变量值更改
			  ```scss
			  $primary-color: #ff0000;
			  
			  .btn-primary {
			      color: $primary-color;
			  }
			  
			  .item {
			      $primary-color: #00ff00;
			      color: $primary-color;
			  }
			  
			  .wrapper {
			      color: $primary-color;
			  }
			  
			  /*
			  .btn-primary {
			    color: #ff0000;
			  }
			  
			  .item {
			    color: #00ff00;
			  }
			  
			  .wrapper {
			    color: #ff0000;
			  }
			  */
			  ```
			- 变量运算
			  ```css
			  /* SCSS 本身支持加减乘元素，其他需要借助math模块 */
			  $width: 100px + 20px;
			  
			  @use "sass:math";
			  // sass 除法 推荐使用math.div函数
			  
			  // 颜色运算相关模块
			  @use "sass:color";
			  
			  // 字符串处理
			  @use "sass:strings";
			  /* 字符串拼接 */
			  $hello: "hello";
			  $world: "world";
			  
			  $foo: $hello + ", " + $world;
			  
			  @debug $foo;
			  ```
		- 规则嵌套
		  collapsed:: true
			- 基本嵌套，显式的表示样式规则的层次关系
			  ```scss
			  .container {
			    width: 100%;
			    .title {
			      font-size: 24px;
			      color: #333333;
			    }
			  }
			  ```
			- 伪类 & 伪元素
			  ```scss
			  a {
			    position: relative;
			    display: inline-block;
			    &:hover {
			      background-color: red;
			    }
			    &::after {
			      content: "";
			    }
			  }
			  ```
			- 父级选择器，`&`符号用于引用父级选择器，在嵌套规则内使用。`&`符号代表所有父层级，而不仅仅代表最近一个层级
		- 指令
		  collapsed:: true
			- 流程控制
			  collapsed:: true
				- 条件判断，`@if`、`@else if`、`@else`
				  ```scss
				  /* condition可以是任何布尔表达式 == != > < and or not */
				  @if <condition> {
				    // 条件为真，执行此处样式
				  } @else if <condition> {
				    // 此处条件为真，执行此处样式
				  } @else {
				    // 否则
				  }
				  
				  $btn-primary-color: green;
				  .btn {
				    @if $btn-primary-color == green {
				      background-color: green;
				    } @else if $btn-primary-color == red {
				      background-color: red;
				    } @else {
				      background-color: blue;
				    }
				  }
				  ```
				- 循环控制
					- `@for`
					  ```scss
					  // @for, $variable 为循环变量，用于迭代中操作，start和end为起始值和结束值
					  @for $variable from <strat> through <end> {
					    // 循环体
					  }
					  // through和to区别：through包含start和end值，to仅包含start，不包含end
					  @for $variable from <strat> to <end> {
					    // 循环体
					  }
					  ```
					- `@each`
					  ```scss
					  // @each list 用逗号或空格分割的值集合
					  @each $variable in <list> {
					    // 循环体
					  }
					  $colors: green, red, black;
					  @each $color in $colors {
					    .bg-#{$color} {
					      background-color: $color;
					    }
					  }
					  @each $key, $value in <map> {
					    // 循环体
					  }
					  $colors: (primary: #cc0000, secondary: #00cc00);
					  @each $name, $color in $colors {
					    .btn-#{$name} {
					      color: $color;
					    }
					  }
					  // 映射多个变量
					  @each $val1, $val2, $val3 in (10px, 20px, 30px), 
					                               (40px, 50px, 60px) {
					    .box-#{$val1}-#{$val2}-#{$val3} {
					      margin: $val1;
					      padding: $val2;
					      border-width: $val3;
					    }
					  }
					  
					  $fonts: 'Arial, sans-serif' 'Georgia, serif';
					  
					  @each $font in $fonts {
					    $prefix: '';
					    @debug string.index($font, 'Arial');
					    @if string.index($font, 'Arial') != null {
					      $prefix: 'heading';
					    } @else if string.index($font, 'Georgia') != null {
					      $prefix: 'body';
					    } @else {
					      $prefix: 'other';
					    }
					    .font-#{$prefix} {
					      font-family: $font;
					    }
					  }
					  ```
					- `@while` 用于创建基于条件的循环指令
			- 混入指令，用于定义可重用块。`@mixin` 定义混合器，`@include` 在选择器内使用混合器
			  ```scss
			  // 创建一组可重用的样式块
			  @mixin <name1> {
			    // property
			  }
			  
			  // 参数化 mixin
			  @mixin <name2>(arg1, arg2) {
			    prop1: arg1;
			    prop2: arg2;
			  }
			  
			  .wrapper {
			    // 引入 mixin
			    @include <mixin name1>;
			    // 设置参数
			    @include <mixin name2>(black, 14px);
			  }
			  ```
			- 函数，用于处理复杂样式计算和生产动态样式。`@function`定义函数，`@return` 定义函数返回值，`call` 用于函数调用
			  ```scss
			  // 自定义函数
			  @function calc-width($width, $count) {
			    return math.div($width, $count);
			  }
			  
			  // 使用函数
			  .column {
			    width: calc-width(800px, 4);
			  }
			  ```
			- 继承 `@extend`，可以将一个选择器样式规则拓展（继承）到另一个选择器上。
			  ```scss
			  .flex-center {
			    display: flex;
			    justify-content: center;
			    align-items: center;
			  }
			  
			  .absolute {
			    position: absolute;
			  }
			  
			  .wrapper {
			    // extend 支持多个选择器继承
			    @extend .absolute, .flex-center;
			  }
			  
			  /* sass 编译结果 */
			  .flex-center, .wrapper {
			    display: flex;
			    justify-content: center;
			    align-items: center;
			  }
			  
			  .absolute, .wrapper {
			    position: absolute;
			  }
			  ```
			- 模块
				- `@import` 最新的 sass3.0 版本已提示`@import`将被废弃，转而使用`@use`指令
				  ```scss
				  @import "variable"; // 没有moudle 概念
				  ```
				- 引入指令，引入外部文件或模块，~~`@import`~~, `@use`
				  ```scss
				  @use "sass:math"; // 类似于js中模块的概念
				  @use "variable" as *; // 全部导入变量文件
				  ```
			- 其他
				- `@media` 媒体查询，根据设备特性和屏幕条件应用不同样式规则。`@media`可嵌套在 Sass 样式表中。
				  ```scss
				  // 媒体查询变量
				  $medium-screen: "(min-width: 768px) and (max-width: 1024px)";
				  
				  .container {
				    width: 100%;
				    .inner {
				      font-size: 16px;
				    }
				  
				    @media screen and (min-width: 768px) {
				      width: 90%;
				      // 嵌套规则，当屏幕宽度大于等于768px时，inner的字体大小变为17px
				      .inner {
				        font-size: 17px;
				      }
				    }
				    
				    // 使用变量
				    @media screen and #{$medium-screen} {
				      width: 80%;
				      .inner {
				        font-size: 18px;
				      }
				    }
				  
				  }
				  
				  /* 编译结果 */
				  .container {
				    width: 100%;
				  }
				  .container .inner {
				    font-size: 16px;
				  }
				  @media screen and (min-width: 768px) {
				    .container {
				      width: 90%;
				    }
				    .container .inner {
				      font-size: 17px;
				    }
				  }
				  @media screen and (min-width: 768px) and (max-width: 1024px) {
				    .container {
				      width: 80%;
				    }
				    .container .inner {
				      font-size: 18px;
				    }
				  }
				  ```
				- 输出，用于控制编译时的输出。`@debug`, `@warn`, `@error`
				  ```scss
				  $width: 80px;
				  @debug $width;
				  ```