- Node内存管理基本知识
	- Node基于V8引擎的Js运行环境，V8内存分配主要分为两个区域：
		- 新生代（`Young Generation`），用于存储生命周期短的小对象。
		  logseq.order-list-type:: number
		- 老生代（`Old Generation`），用于存储生命周期长的大对象。
		  logseq.order-list-type:: number
	- V8内存默认限制为1.5G内存（实际有待商定）。
		- 查看默认设置
		  logseq.order-list-type:: number
			- logseq.order-list-type:: number
			  ```javascript
			  ```
		- `node --max_old_space_size=<size>` 设置老生代内存上线，以MB为单位。`max_old_space_size`不应该超过物理机内存大小，否则会导致系统频繁Swap。
		  logseq.order-list-type:: number
- 内存泄露排除
	- `heapdump`
	  logseq.order-list-type:: number
	- `node --inspect`
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number