- 类型
  id:: 696df7de-299b-41db-b493-7a0de6a9abd2
	- Js中分为基本类型和引用类型。
	  logseq.order-list-type:: number
	- 基本类型（除null、undefined、symbol、bigint外）存在与之对应包装类型。
	  logseq.order-list-type:: number
	- 不同数据类型之间的转换
	  logseq.order-list-type:: number
		- 显示转换
		  logseq.order-list-type:: number
		- 隐式转换
		  logseq.order-list-type:: number
	- 判断数据类型的基本方法
	  logseq.order-list-type:: number
		- 基本数据类型：`typeof`、`globalThis.isNaN`、`Number.isNaN`
		  logseq.order-list-type:: number
		- 引用数据类型：`instanceof` 仅适用于**对象初始化在相同上下文中**
		  logseq.order-list-type:: number
			- [[instanceof原理]]
			  logseq.order-list-type:: number
		- 通用方法：`Object.prototype.toString.call([])` 用于查看对象内部的`[[Class]]`值，可适用于不同上下文中判断变量类型，但无法判断派生对象。
		  logseq.order-list-type:: number
	- logseq.order-list-type:: number
-