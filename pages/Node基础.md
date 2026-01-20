- 特性：事件机制、异步 IO
- 模块：在 Node 环境中，一个文件便是一个模块，文件路径即是模块名。
  collapsed:: true
	- `commonjs`，node 原生模块加载机制，
		- 三个原生预定义变量：
			- `require` 用于加载和使用其他模块。
			- `exports` 用于导出模块中的公共属性和方法`exports.hello = function() {}`。
			- `module` 用于访问当前模块相关信息，最常用的用途是**替换当前模块的导出对象`module.exports = {}`**，默认导出对象会被替换一个`{}`。
		- 模块初始化：
			- 一个模块中的 JS 代码**仅在模块第一次被 require**时被执行，并初始化被导出的对象，之后，**缓存**起来可被重复利用。
		- 主模块
			- 通过命令行参数传递给 Node 执行的模块被称为主模块。
	- `es module`，
	-
- Node 模块路径解析规则，require支持相对或绝对路径导入：
  collapsed:: true
	- 内置模块
	- `node_modules`，用于存在 node 包，node 会尝试当前`package.json`所在模块加载，如果没找到则向上一级目录，直至跟目录为止。
	- `NODE_PATH`环境变量，Node 允许指定`NODE_PATH`环境变量指定额外的模块搜索路径，可指定一个或多个目录路径（Linux 下使用`:`分割，Windows 下使用`;`分割）。
- package（包）
	- 在node中自定义模块，需要在项目根目录中创建`package.json` 文件
		- ```json
		  {
		    "name": "package name",
		    "mian": "./lib/index.js" // 指定入口模块文件
		  }
		  ```
		- `pac`指定一个包的入口文件
	- 命令行程序
	  collapsed:: true
		- 在 Linux 系统中，可以把 JS 脚本当做 Shell 脚本运行
			-
			- ```javascript
			  #! /usr/bin/env node
			  // #! 注释是用来指定当前脚本使用的解析器。
			  // Nodejs 会自动忽略掉#!注释
			  ```
			- `chmod +x /home/user/bin/node-echo` 赋予脚本执行权限
		- 在 Window 系统中需要使用`cmd`文件解决
			- ```cmd
			  @node "C:\User\user\bin\node-echo.js" %*
			  ```
	- `NPM`，npm 是随 node 一起安装的**包管理工具**
	  collapsed:: true
		- 应用场景：
			- 允许用户从 npm 服务器上下载第三方包到本地；
			- 允许用户从 npm 服务器上下载第三方命令行到本地；
			- 允许用户将自己的包或命令行上传到 npm 或私人服务器上；
- 文件操作
- 网络操作
- 进程管理