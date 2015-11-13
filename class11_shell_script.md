#Shell scripting

- shell script是命令的集合

- 通常，运行shell script时，shell会fork出一个子shell来跑

- 但是，如果用`.`或者`source`来运行，则shell会在当前环境下跑该脚本。在一些需要设置环境/环境变量的脚本的执行时，就要用这个，比如`~/.bashrc`里配置了一些东西，需要立即生效，就可以`. ~/.bashrc`或者`source ~/.bashrc`来达到目的。
 - `.`和`source`等价，都是shell内建(built-in)命令。

- shell命令行参数
 - $#代表参数个数，不包含脚本名本身
 - $1,$2,...$($#)表示各参数，从1开始计数，不包含脚本名本身。

- 输入输出重定向中，没有`<<`，此处说明其特殊用途。
 - `<< final`可指定结束标记，举例说明:
 	- `cat << final > tmp.txt`，可从键盘读入字符放入`tmp.txt`，`<< final`的功能就是当且仅当遇到单独的一行，改行仅包含`final`(除结尾换行符外，没有任何其他字符，**不能包含空白符**)时，读入结束，`final`本身不会读入，效果相当于`EOF`(`Ctrl-D`)。
 - `xargs`，该命令可以将得到的输入变成多个参数传递给后面的命令，按照`arg1 arg2 arg3 ...`的形式给出.如`find . -type -f | xargs chmod 664`，等价于`find . -type -f -exec chmod 664 {} \;`。

- `test`命令
 - `[]`可以达到和`test`相同的功能，用得更多一些, e.g.
 ```bash
 if [ $cnt -le 15 ]; then
	 echo $cnt
	 cnt=$(($cnt+1))
 fi
 ```

 | 选项 | 功能 |
 |:----:|:--------------------:|
 | -f | 是否为文件 |
 | -d | 是否为目录 |
 | -r | 是否可读 |
 | -w | 是否可写 |
 | -x | 是否可执行 |
 | -s | 文件长度是否大于0(是否为空) |
 | -n | 字符串是否不为空 |
 | -z | 字符串是否为空 |
 | == | 判字符串相等 |
 | != | 判字符串不等 |
 | -eq | 数值比较equal |
 | -ne | not equal |
 | -lt | less than |
 | -le | less than or equal |
 | -gt | greater than |
 | -ge | greater than or equal |

- `&&`和`||`
 - 可用来连接命令，注意`||`的**短路**效应，比如`[ -f dong.txt ] || echo 'dong.txt not exist' && echo 'dong.txt exist'`，如果`dong.txt`存在，则`echo 'dong.txt not exist'`不会执行(被短路), 于是`[ -f dong.txt ]`的返回值会继续向后传递，`&&`后命令当且仅当前面的返回值为`0`时才会执行，于是`echo 'dong.txt exist'`就会打印粗来惹。

- `if-else`控制结构
 ```bash
 if condition
 then do-something
 fi
 ```

- `while`循环
 ```bash
 while condition
 do something
 done
 ```

- `for`循环
 - e.g.
 ```bash
 for file in ~/*; do
 	echo $file
 done
 ```
- 循环处理参数
 - 当需要处理每一个script参数时...
 - `shift`可在执行后，将所有参数左移，$#减少1，剩余参数还从1开始编号..
 - `eval echo \$$x`，两次解析，假设`x=1`，第一次解析出`echo $1`，第二次就可以打印第1个参数了

- `read`命令
 - 从`STDIN`读取，存入后面指定变量, `-p`选项可加提示语。

- `let`和`$(())`
 - 用于四则运算，经常用在如变量增1，求和等等。
 - e.g.
 ```bash
 let x=$y+$z
 ```
  等价于
 ```bash
 x=$(($y+$z))
 ```
 - `expr`也可用于计算

- 命令查找过程
 - 是否为Qualified path name。如`/bin/ls -l`，指定了路径，此时**无任何歧义**, 执行的一定为`/bin/`下名为`ls`的程序
 - Reserved word, 保留字。如`do`, `done`, `if`...
 - Alias
 - Built-in command, 内建命令。如`source`, `[`, `((`, `(`, ...
 - Function.
 - PATH环境变量。按照从前往后的顺序依次查找。

