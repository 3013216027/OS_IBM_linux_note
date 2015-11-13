#Linux utilities

- Include commands: find & locate, grep, cut, sort, head, tail, type, which, whereis, file, join, paste, etc. 最重要的是`find`和`grep`

### find
- `find where what how`, e.g. `find . -name orange`
- `find`默认会递归地查找
- `find . -name 's*' -exec ls -i {} \;`, `-exec`和`\`为固定组合，中间部分为命令，`{}`为占用符，表示将找到的结果填入该位置（而不是`-i`前或其他地方）.
 - 注意，通配符，如`*`在输入命令后，由终端处理后交给相应程序，于是假设上述命令中，`s*`没有加引号，则`find`处理时得到的命令中，`s*`会被该目录下的`s`开头的文件/文件夹名字所替换，可能会导致语法或结果错误，当且仅当`s*`匹配且仅匹配当前文件夹下的一个名字时，结果才正确。`find`可自己处理这个通配符，而其他命令如`ls s*`，`*`号实际上是被bash预先处理掉的= =
- `find . -name o\* -ok rm {} \;`, `-ok`参数可以在每执行一组后向用户询问一次.
 - 此处的询问由`find`发起，若得到确认，才交给后者处理，而`rm -i`则是在处理过程中询问，二者有所不同。
- 常用参数
 - 选项之间可以用`-a`(and), `-o`(or)逻辑连接

 | 选项 | 参数 | 功能 |
 |:------:|:-------:|:-----------------------:|
 | -type | f,d | 文件(Ordinary file), 文件夹(Directory) |
 | -size | +n,-n,nc | 大于n blocks, 小于n blocks, 等于n characters |
 | -mtime | +n,-n,n | n天前修改,n天内修改,n天时修改 |
 | -perm | onum,mode | 权限符合onum/mode |
 | -user | user | 找所有者为user的文件 |
 | -newer | ref.file | 在最后一次修改ref.file后修改的文件 |
 | -o, -a | | 逻辑或/逻辑与 |
- locate

### grep与正则表达式
- `grep`常用选项

 | 选项 | 功能 |
 |:----:|:----------:|
 | -i | 忽略大小写 |
 | -v | 取反匹配,用得最多 |
 | -w | 全字匹配 |
 | -x | 全行匹配 |
 | -c | 只打印匹配次数(不打印具体匹配到的行内容) |
 | -n | 结果中显示行号 |

 - 各种搞，此处不再赘述
