- **PostCSS**是一个用于对 CSS 进行转换和处理的工具。相较于Sass 等方案，PostCSS 并未引入新语法拓展 CSS ，而是通过 Js 插件来处理 CSS。
- **PostCSS**用途
  collapsed:: true
	- 兼容性处理
		- `autoprefixer` 特定浏览器前缀
		- `postcss-cssnext` 使用最新 CSS 语法
	- 单位转换（px2rem、px2viewport）
	- 压缩 CSS 文件
		- `cssnano` 移除注释、空白、重复规则、过时的浏览器前缀
	- 图片处理
		- `postcss-assets` 处理尺寸、内联图像（base64 url）、清除缓存
- PostCSS 安装&用例
  collapsed:: true
	- PostCSS 安装
	  ```bash
	  pnpm add postcss autoprefixer stylelint 
	  ```
	- `Webpack`配置
	  collapsed:: true
		- 配置文件，在项目根目录下创建`postcss.config.js`文件
		  ```javascript
		  // pnpm add -D postcss-load-config
		  /** @type {import('postcss-load-config').Config} */
		  module.exports = {
		    plugins: [
		      require('stylelint'),
		      require('autoprefixer')
		    ]
		  };
		  ```
		- 配置`webpack.config.js`
		  ```javascript
		  module.exports = {
		    // ...
		    module: {
		      rules: [
		        {
		          test: /\.css/$,
		          exclude: /node_modules/,
		          // postcss-loader 会自动寻找项目跟路径下的 config 文件，也可在此处配置
		          use: ['style-loader', 'css-loader', 'postcss-loader'],
		        }
		      ]
		    }
		  };
		  ```
	- `Gulp`配置
	  collapsed:: true
		- 安装基本插件
		  ```bash
		  pnpm add -D gulp gulp-postcss gulp-sourcemap postcss-reporter
		  pnpm add -D stylelint-config-standard
		  ```
		- 配置`gulp.config.js`文件
		  ```javascript
		  const gulp = require('gulp');
		  const buildCss = () => {
		    const postcss = require('gulp-postcss');
		    const sourcemaps = require('gulp-sourcemaps');
		    const stylelint = require('stylelint');
		    const reporter = require('postcss-reporter');
		    const autoprefixer = require('autoprefixer');
		    return gulp.src('src/styles/*.css')
		        .pipe(sourcemaps.init())
		        .pipe(postcss([
		            stylelint({
		                config: {
		                    extends: 'stylelint-config-standard',
		                    customSyntax: 'postcss-lit'
		                }
		            }),
		            autoprefixer(),
		            reporter({clearAllMessages: true}),
		        ]))
		        .pipe(sourcemaps.write('.'))
		        .pipe(gulp.dest('dist/styles'));
		  };
		  gulp.task('build:css', buildCss);
		  ```
- PostCSS 插件
  collapsed:: true
	- 插件调用
	  ```javascript
	  // 不借助webpack、glup 等打包工具，使用 js api
	  const postcss = require('postcss');
	  const autoprefixer = require('autoprefixer');
	  
	  const code = `.example {
	      display: flex;
	      transition: all 0.3s ease;
	  }`;
	  
	  const process = async () => {
	    	// postcss 插件调用顺序按照 数组或 use 的声明顺序
	      const result = await postcss([autoprefixer])
	          .process(code, { from: undefined });
	      console.log(result.css);
	      // 插件可以通过数组方式传递，也可使用 postcss 的 use 函数
	      const result2 = await postcss()
	          .use(autoprefixer)
	          .process(code, { from: undefined });
	      console.log(result2.css);
	  }
	  
	  process();
	  ```
	- 常见插件
	  collapsed:: true
		- `Autoprefixer`，是一个流行的前缀自动添加工具，能够根据指定的浏览器目标范围自动为 CSS 代码创建需要的浏览器前缀。工作原理是基于 **Can I Use** 上的数据，它会根据你设置的目标浏览器版本，自动检测和添加相应的浏览器前缀。
		- `Stylelint` 代码规范问题
		- `cssnano` 代码压缩
		- `postcss-import` 支持使用`@import`导入其他 css 文件
		- `postcss-url` 处理 css 中的 url，自动重写或内联文件
		- `postcss-px-to-rem` 将 px 转化为 rem 单位
	- 、PostCSS 插件可以是一个**函数**，也可以是一个**对象**。
	  ```javascript
	  /**
	   * 实现一个简单PostCSS 插件，实现在文件顶部添加注释和@charset
	   * @param {import('postcss').Root} root 
	   */
	  function mySimplePlugin(root) {
	      root.prepend({ type: 'comment', text: 'Processed by My Simple Plugin' });
	      root.prepend({ type: 'atrule', name: 'charset', params: '"UTF-8"' });
	      return root;
	  }
	  
	  module.exports = { mySimplePlugin };
	  ```
	- CSS语法类型
	  | 类型 | type值 | 说明 |
	  | --- | --- | --- |
	  | 规则集（Rule）| rule | CSS规则由选择器和声明块组成 |
	  | 注释（Comment）| comment | 由`/**/`声明 |
	  | @规则（At Rule）| atrule | `@import`、`@media`、`@font-face`等规则 |
	  | 声明（Declaration）| decl | CSS 声明块中具体的样式属性和值 |
	  | 根（root）| root | 整个 CSS 文档 |
	- 插件常用 API
	  collapsed:: true
	  PostCSS 插件既可以是一个函数也可以是一个对象，处理较为复杂逻辑时建议使用对象形式。
		- Plugin 对象相关钩子函数
		  ```javascript
		  /**
		   * 实现一个 Object 类型的插件
		   * @returns {import('postcss').Plugin}
		   */
		  function myObjectPlugin(...args) {
		      return {
		          postcssPlugin: 'my-object-plugin',
		          Once(root, { result }) {
		              // 只调用一次，表示插件初始化，用于初始化操作
		              console.log('Once');
		          },
		          Root(root, { result }) {
		              // 对根节点进行处理或修改，解析 Root 类型时会被调用
		              console.log('Root');
		          },
		          Declaration(decl, { result }) {
		              // 对声明节点进行处理或修改，解析 Declaration 类型时会被调用
		              console.log('Declaration');
		          },
		          DeclarationExit(decl, { result }) {
		              // 对声明节点的退出进行处理，解析 DeclarationExit 类型时会被调用
		              console.log('DeclarationExit');
		          },
		          AtRule(atRule, { result }) {
		              // 处理 @ 规则的参数和内容
		              console.log('AtRule');
		          },
		          AtRuleExit(atRule, { result }) {
		              // 处理 @ 规则的退出
		              console.log('AtRuleExit');
		          },
		          Rule(rule, { result }) {
		              // 处理规则的选择器和内容
		              console.log('Rule');
		          },
		          RuleExit(rule, { result }) {
		              // 处理规则的退出
		              console.log('RuleExit');
		          },
		          Comment(comment, { result }) {
		              // 处理注释
		              console.log('Comment');
		          },
		          CommentExit(comment, { result }) {
		              // 处理注释的退出
		              console.log('CommentExit');
		          },
		      }
		  }
		  
		  // 这样插件即可当函数直接被调用，也可进行参数配置
		  myObjectPlugin.postcss = true;
		  
		  module.exports = { myObjectPlugin };
		  ```
		- 节点相关 api
			- 容器方法（root、node、rule）
				- `insetAfter` 在某个节点后面添加。
				- `insertBefore` 在某个节点前面添加。
				- `append` 添加到容器的最后面
				- `prepend` 添加到容器的最前面
				- `after` 指当前节点的父容器调用，相当于`node.parent.insertAfter`
				- `brefore` 指当前节点的父容器调用，相当于`node.parent.insertBefore`
			- 节点方法（decl）注：容器节点也可以调用
				-
				-
- PostCSS 基础原理
  collapsed:: true
	- 前置知识
		- AST树，AST 本质上是一个 Js 对象，将 CSS 代码转为一种树形结构，树的每个节点表示 CSS 不同部分，如规则集（rule）、选择器（selector）、属性（decl） 等。通过遍历和操作 AST ，可以对 CSS 进行转换和处理。
		- postcss 解析 css 代码
		  ```javascript
		  const postcss = require('postcss')
		  const ast = postcss.parse(`.box { display: flex; }`)
		  ```
	- Node属性
	  postcss 在完成解析 css 代码后，会返回一个`root`对象（代表整个 css 文档）。其中有几个需要注意的属性
	  ```javascript
	  // parse函数返回的 root 节点
	  {
	      // ...
	      nodes: [
	          { /** rule/atrule对象，css 选择器经 postcss 转化后的 js 对象 */ },
	          // ...
	      ],
	  }
	  
	  // 单个 rule 节点
	  {
	      type: 'rule', // 节点类型 - 规则
	      selector: '.example', // 选择器
	      nodes: [
	          {
	              type: 'decl', // 节点类型 - 声明
	              prop: 'color', // 属性
	              value: 'red' // 属性值
	          },
	          // ...
	      ]
	  }
	  ```
	-