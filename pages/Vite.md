- Vite 快速打包工具，核心原理：利用现代浏览器的原生系统模块 ESM（ES Modules）。
	- 开发环境，Vite将请求资源进行拦截，并使用`esbuild`对源码进行实时编译和构建，不需要将代码进行整体打包。
	- 正式环境，使用`rollup`对源码进行打包处理。
- ((68b54eba-8e18-4cbc-80c9-3a5f41d71e66))
- 样式处理
  id:: 68b55335-e6e1-4fb4-8551-e778f0e3a146
	- CSS 处理
	  collapsed:: true
		- Vite 内部内置了对 CSS 的简单处理
		- 使用 PostCSS
		  ```bash
		  # 安装
		  pnpm add -D postcss autoprefixer
		  ```
		  项目根目录下配置有效的 PostCSS 配置（`postcss.config.js`），vite 会自动将其应用到已导入的 css。
		  ```javascript
		  // postcss.config.js
		  module.exports = {
		    plugins: {
		      autoprefixer: {
		        overrideBrowserslist: ['defaults', 'not dead', 'ie >= 8'],
		        grid: true,
		      }
		    }
		  };
		  ```
	- 预处理器
	  Vite 同时提供了对`.scss`, `.sass`, `.less`, `.style`等文件的内置支持。但必须安装相对应的**预处理器**依赖。
	  ```bash
	  pnpm add -D sass
	  ```