- Node服务内存排查
	- [Node.js 微服务内存泄漏的排查与解决-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2563078?policyId=1004)
	- [排查 Node.js 日志报错：内存溢出问题解决实战-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2566646?policyId=1004)
- 异步迭代器（EventEmitter）
  id:: 695c84ee-b8e2-4918-a6e4-6efef9bcb789
	- `EventEmitter.on(emitter, eventName)`方法会返回`eventName`的可迭代对象，可使用`for...of`迭代该`emitter`触发`eventName`事件。当`emitter`触发`error`事件时，迭代器会抛出异常。
	  ```javascript
	  import EventEmitter from "node:events";
	  
	  function Logger() {
	    
	  }
	  ```