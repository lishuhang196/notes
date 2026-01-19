- Node服务内存排查
	- [Node.js 微服务内存泄漏的排查与解决-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2563078?policyId=1004)
	- [排查 Node.js 日志报错：内存溢出问题解决实战-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2566646?policyId=1004)
- 异步迭代器（EventEmitter）
  id:: 695c84ee-b8e2-4918-a6e4-6efef9bcb789
  collapsed:: true
	- `EventEmitter.on(emitter, eventName)`方法会返回`eventName`的可迭代对象(`AsyncIterator`)，可使用`for...of`迭代该`emitter`触发`eventName`事件。当`emitter`触发`error`事件时，迭代器会抛出异常。
	- 代码示例
	  collapsed:: true
		- ```javascript
		  import EventEmitter from "node:events";
		  import util from "node:util";
		  
		  function Logger() {
		    EventEmitter.call(this);
		  }
		  
		  // 继承EventEmitter类，Logger.prototype = Object.create(EventEmitter.prototype)
		  util.inherits(Logger, EventEmitter);
		  
		  Logger.prototype[Symbol.asyncIterator] = function () {
		    const self = this;
		    return EventEmitter.on(self, "line");
		  }
		  
		  Logger.prototype.log = function (message) {
		    const self = this;
		    self.emit('line', message);
		  };
		  
		  const logger = new Logger();
		  
		  process.nextTick(function () {
		    logger.log("\x1b[33mThis is a log message.\x1b[0m");
		    logger.log("\x1b[32mThis is another log message.\x1b[0m");
		  })
		  
		  // 打印
		  for await (const item of logger) {
		    console.log(item[0]);
		  }
		  ```
	-
- [[异步流处理]]
-