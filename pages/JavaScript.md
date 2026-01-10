- Javascript 模块化
  collapsed:: true
	- ((68a4341f-38e6-4451-b334-61dcbe002123))
	- `ES Module` 知识点
	  id:: 68b54eba-8e18-4cbc-80c9-3a5f41d71e66
	  ```html
	  <!-- 浏览器 -->
	  <script type="module" src="xxx.js"></script>
	  <script type="module">
	    /** 浏览器会对内部的 import 引用发起 http 请求获取模块内容 */
	    import $ from 'jquery';
	  </script>
	  <script type="module">
	    // 多次引入相同模块，模块内部只会执行一次
	    import $ from 'jquery';
	  </script>
	  ```
- 严格模式
  collapsed:: true
	- 严格模式：在**Js文件或函数头部**使用`"use strict";`
	- 严格模式和正常模式区别
	  | | 严格模式 | 正常模式 |
	  | --- | --- | --- |
	  | delete 不存在的标识符  | 抛出语法错误，禁止删除变量  | 静默失败并返回 false |
	  | 在**对象直接量**中定义同名属性 | 抛出语法错误 | 前声明属性被覆盖 |
	  | 函数参数同名 | 语法错误 | 前声明参数被覆盖 |
	  | arguments 对象 | 传入函数内部实参列表的静态副本（修改 arguments 对象属性值不会导致实参变化）| arguments 对象里的元素和对应的实参是指向同一个值的引用 |
	  | eval 和 arguments |  关键字，不能被赋值或用作变量声明 | ~ |
	  | eval |  eval 函数执行的代码内部变量会绑定在**eval 作用域**中，外部无法使用 | 正常模式下，eval 语句的作用于取决于其位置（全局或函数作用域） |
	  | 调用栈检查 (arguments.callee、arguments.callee.caller) | 抛出异常TypeError | 正常访问 |
	  | 变量声明 | 变量必须先声明在使用，无法使用 with 关键字 | 直接给变量赋值，会隐式创建全局变量 |
	  | call/apply | 调用时传入 null、undefined 会保持原样，不被转换为 window | 函数 this 会指向 gloablThis 对象 |
	-
	- 禁止 this 关键字指向全局对象（正常模式下，函数执行时内部 this 执行 globalThis 对象）
	- 对**禁止拓展的对象（`Object.preventExtensions(obj)`）**或**冻结的对象（`Object.freeze(obj)`）**添加新属性会报错。
	-
- 基本语法
	- 数据类型
		- 原始数据类型，直接存储在**栈内存**中，一般保存函数参数、局部变量等，由编译器自动分配和释放。
		  栈内存特点：内存空间小、大小固定、操作频繁。
			- `Undefined`，只有一个**唯一字面值 `undefined`，标识一个变量**未被初始化**。
			  collapsed:: true
				- 出现`undefined`的场景
				  collapsed:: true
					- 使用只声明未初始化的变量时，返回 undefined；
					- 获取一个对象的某个不存在的属性（自身属性或原型链继续的属性）；
					- 函数没有明缺的返回值；
					- 函数定义使用多个形参，调用函数时，传递参数数量小于形参数量，未匹配的参数为 undefined
				- `undefined` 是全局对象的一个属性，**不是保留字**，在 ES5 规范中，全局 undefined 可以被重写，而在 ES5 及之后版本，全局 undefined 被设置为只读，但其值在局部变量中当然可被重写。
				  ```javascript
				  Object.getOwnPropertyDescriptor(globalThis, 'undefined')
				  function foo() {
				      // undefined = 123;
				      var undefined = 123;
				      console.log(undefined);
				  }
				  foo();
				  ```
				- `void 0`可以安全获取 undefined 值。
					- `void` 是一个一元运算符，他会对后面的**表达式**求值，但总是返回`undefined`值。
					- 避免重写：`void`运算符本身无法被重写。
					- 代码压缩：`void 0`相较于`undefined`占用字节数量更少，能够减少代码量。
			- `Null`，唯一字面量值 null，标识一个空指针对象。
				- 使用`typeof null`检查 null 值时，会返回`object`字符串。
				-
			- `Boolean`
			- `Number` 64 位浮点数、8 字节（`Number.MAX_SAFE_INTEGER` 最大安全整数 `Number.MIN_SAFE_INTEGER` 最小安全整数）
			- `String`
			- `Symbol` 代表独一无二且不可变的数据类型，主要作用：1. 避免全局变量冲突；2. 对象内部变量覆盖（`Symbol.iterator`）
			- `Bigint` 任意精度正整数，安全的存储和操作大数。
		- 引用数据类型，存储在堆内存中，通过指针引用，需要手工或垃圾回收释放。
		  堆内存特点：内存空间大、大小不固定。
			- `Object`（`Array`、`Function`、`Date`）
	- 变量
	-
	- 操作符 & 操作符
	  collapsed:: true
		- `delete` 操作符
			- 删除对象属性 `delete obj.name` (严格模式下，`delete` 未声明属性报错)
			- 可删除**没有使用 var 关键字声明**的全局变量（直接定义在 window 对象上的属性）
				- 正常模式下，使用 var 定义的变量会静默失败
				  ```javascript
				  var foo = "foo"
				  delete foo; // 静默失败 false
				  delete window.foo; // 也会返回 false
				  ```
				- 严格模式下，报错
			- 使用 delete 删除数组元素，不会改变数组长度，被删除的元素使用`empty`代替
			- 不能删除内置对象属性
			- 不能删除从`prototype`上继承的属性
	- 语句
- 函数 & 作用域 & 闭包
- 对象
- 异步 & 网络请求
- ES6
	-