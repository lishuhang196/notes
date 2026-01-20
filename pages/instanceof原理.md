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