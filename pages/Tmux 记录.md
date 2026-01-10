- Tmux 基本概念
	- `Session`，会话
		- 普通终端中 session 和 window 绑定，当所有 window  关闭后，session 也随着关闭，session 内部**所有的进程**也会随之终止。
		- Tmux 就是就能够将 session 放置于后台运行。
	- `Window`，窗口（工作区）
		- 一个 session 中可以创建多个 window，
	- `Panel`，窗格
		- 一个 window 中可以创建多个 panel
- Tmux 安装
  ```bash
  # macos 安装
  brew install tmux
  # linux
  sudo apt install tmux
  ```
- Session 操作
	- 启动 Tmux
	  ```bash
	  # 默认启动
	  tmux
	  # 为 session 命名
	  tmux new -S <session name>
	  
	  # 显示所有会话
	  tmux ls
	  
	  # 快捷键，列出所有 session，并切换
	  <Ctrl + b> s
	  ```
	- 分离（后台运行session）
	  ```bash
	  tmux detach
	  
	  # 快捷键，tmux 命令默认前缀为<Ctrl + b>
	  <Ctrl + b> d
	  ```
	- 退出
	  ```bash
	  # 关闭所有session
	  tmux kill-server
	  
	  # 关闭指定session
	  tmux kill-session -t <session name>
	  
	  # 关闭除指定 session 的所有会话
	  tmux kill-session -a -t <session name>
	  ```
	- 绑定/切换/重命名 session
	  ```bash
	  # 重新绑定指定session
	  tmux attach -t <session name>
	  
	  # 切换session
	  tmux switch -t <session name>
	  
	  # 重命名 session
	  tmux rename-session -t <old session> <new session>
	  ```
- Window 操作
	- 新建/罗列/切换 窗口
	  ```
	  # 新建窗口
	  <Ctrl + b> c #快捷键创建一个新窗口
	  tmux new-window -n <window name> #新建一个指定名称窗口
	  
	  # 列出所有窗口
	  ```
- Panel 操作