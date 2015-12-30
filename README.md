# This is JBer's linux class notes.
- Start from class-8
- 复习内容 3.4.5.8.9.10.11

### 目录
- class08: shell基础。介绍通配符，文件重定向(管道)，基本命令(`grep`, `ps aux`等)，shell全局变量($$, PATH, PS1-4, PWD, HOME, LANG), 命令重命名`alias`
- class09: 进程。介绍父子进程，进程控制(工作`job`控制，`kill`信号和控制)，进程优先级(`nice`, `renice`)
- class10: 主要介绍`find`和`grep`两个命令。`find`用于查找/搜索文件(并处理)，`grep`用于(基于正则表达式)处理字符串(按行抓取字符串)，另有一个`awk`命令，也用正则表达式匹配处理字符串
- class11: shell脚本。包括几个特殊的变量(`$1`，`$#`等)，`<<`，`test`命令(`[]`与之等价)(用于测试文件是否存在，是否可读/写/执行，字符串/数值比较)，`&&`和`||`，`if-else`控制结构和各种循环，shell对输入命令的处理(查找)过程
