- Node内存管理基本知识
  id:: 696e024d-839e-4e36-840f-79d20a82377e
	- Node基于V8引擎的Js运行环境，V8内存分配主要分为两个区域：
	  collapsed:: true
		- 新生代（`Young Generation`），用于存储生命周期短的小对象。
		  logseq.order-list-type:: number
		- 老生代（`Old Generation`），用于存储生命周期长的大对象。
		  logseq.order-list-type:: number
	- V8内存默认限制为1.5G内存（实际有待商定）。
	  collapsed:: true
		- 查看默认配置
		  logseq.order-list-type:: number
		  collapsed:: true
			- logseq.order-list-type:: number
			  ```javascript
			  import v8 from 'v8';
			  import os from 'os';
			  
			  const heapLimit = v8.getHeapStatistics().heap_size_limit;
			  console.log(v8.getHeapStatistics());
			  console.log('当前堆限制:', Math.round(heapLimit / 1024 / 1024), 'MB');
			  console.log('系统总内存:', Math.round(os.totalmem() / 1024 / 1024), 'MB');
			  ```
		- `node --max_old_space_size=<size>` 设置老生代内存上线，以MB为单位。`max_old_space_size`不应该超过物理机内存大小，否则会导致系统频繁Swap。
		  logseq.order-list-type:: number
	- [[译]你应该知道的 Node.js 内存限制在这篇文章中，我将探索 Node 中的堆内存分配，以及尝试运行本地硬件的极限 - 掘金](https://juejin.cn/post/7087578623393136670)
- 内存泄露排除
	- `heapdump`
	  logseq.order-list-type:: number
	- `node --inspect`
	  logseq.order-list-type:: number
- [Node.js内存管理和V8垃圾回收机制-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/1462409)