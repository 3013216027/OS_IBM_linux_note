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
