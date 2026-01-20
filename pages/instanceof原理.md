- instanceof：检查一个对象的原型链中是否包含某个构造函数的prototype属性
- 仅适用于相同上下文
  ```javascript
  const iframe = document.createElement('iframe')
  document.body.appendChild(iframe)
  // iframe 会产生不同上下文
  const IframeArray = iframe.contentWindow.Array
  const arr = []
  arr instanceof Array // true
  arr instanceof IframeArray // false
  ```
- 产生不同上下文的情况
	- iframe框架
	  每个iframe标签都会创建独立`window`对象，每个`window`对象都存在独立的内置构造函数，因此虽然与父页面构造函数功能相同，但不是同一个函数
	- 浏览器拓展
	- Web Workers，独立全局环境，与主线程隔离
	- 跨域脚本，如果存在沙箱隔离，也会产生上下文差异。
		- 一般是需要结合iframe，创建sandbox沙箱。
		- [[跨域]]
- "如何理解instanceof仅适用对象初..."点击查看元宝的回答
  https://yb.tencent.com/s/TS1QdkmindAg
-