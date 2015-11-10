#进程
- 进程组分

 | 进程 | 进程 |
 |:----:|:----:|
 |PCB|PCB|
 |Text|Text|
 |Data|Data|

 - 每个进程都有自己的环境(environment)

 | Process environment | 环境组分 |
 |:-------------------:|:--------:|
 |Program name|进程名|
 |Internal data|数据|
 |Open files|打开的文件|
 |Current directory|PWD,当前目录|
 |Additional parameters|...|
 |User and group ID|用户和组ID(执行该进程的)|
 |Process ID|PID,进程ID|
 |Parent PID|PPID,父进程的进程ID|
 |Program variables|...|

- 父子关系
 - 父进程创造(fork)子进程，自己休眠(Sleep)
 - 子进程执行(exec)完后死亡(exit)，唤醒父进程
 - 父进程欲终止自己，需要先终止子进程，递归。或者将子进程交给init进程，此时子进程成为init的子进程

- 进程控制
 - 进程状态
 	- 前台运行: 如直接运行时`dd if=/dev/zero of=/dev/null`
	- 后台运行: 命令后加`&`，如`dd if=/dev/zero of=/dev/null &`
	- 后台挂起: 如前台运行时`Ctrl-Z`
	- 前台运行->后台挂起: `Ctrl-Z`
	- 后台运行->前台运行: `fg %1`将1号工作转入前台运行，`fg`讲后台中第一顺位工作转入前台运行
	- 后台挂起->前台运行：`fg %2`
	- 后台挂起->后台运行: `bg %2`
 - 控制有两种方法
 	- 用工作编号(job number),如 `fg %2`
	- 用进程ID(PID)，如`kill 2333`, 向进程2333发射一个终止信号(signal)，当然，其不一定会相应
 - kill信号
 
	 | 信号 | 键盘 | 含义 | 默认动作 |
	 |:----:|:------:|:-------:|:---------:|
	 |01| |挂起,Hangup|终止进程,End process|
	 |02|Ctrl-C|中断,Interrupt|终止进程,End process|
	 |03|Ctrl-\\|退出,Quit|终止进程并转储,End process and core dump|
	 |09| |杀死,kill|终止进程(不可被重定义),End process(Cannot be redefined-handled by kernel)|
	 |15| |终结,Terminate|终止进程,End process|
	 - e.g. `kill -9 2333`x掉2333，没得商量= =

- 相关命令
 - `ps`, 显示当前进程，`ps aux`显示当前系统所有进程
 	 - `-a`: all processes attached to a terminal
	 - `-x`: all other processes
	 - `-u`: provides more columns
 - `pstree`, 显示进程树

