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
