#Linux utilities

- Include commands: find & locate, grep, cut, sort, head, tail, type, which, whereis, file, join, paste, etc.

### find
 - `find where what how`, e.g. `find . -name orange`
 - `find`默认会递归地查找
 - `find . -name 's*' -exec ls -i {} \;`, `-exec`和`\`为固定组合，中间部分为命令，`{}`为占用符，表示将找到的结果填入该位置（而不是`-i`前或其他地方）.
 	 - 注意，通配符，如`*`在输入命令后，由终端处理后交给相应程序，于是假设上述命令中，`s*`没有加引号，则`find`处理时得到的命令中，`s*`会被该目录下的`s`开头的文件/文件夹名字所替换，可能会导致语法或结果错误，当且仅当`s*`匹配且仅匹配当前文件夹下的一个名字时，结果才正确。`find`可自己处理这个通配符，而其他命令如`ls s*`，`*`号实际上是被bash预先处理掉的= =
 - `find . -name o\* -ok rm {} \;`, `-ok`参数可以在每执行一组后向用户询问一次.
 	- 此处的询问由`find`发起，若得到确认，才交给后者处理，而`rm -i`则是在处理过程中询问，二者有所不同。
