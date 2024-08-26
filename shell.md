# Bash Shell
1. What is Shell?  
    - shell是运行在终端中的文本互动程序。
    - shell是用户和Linux（或者更准确的说，是用户和Linux内核）之间的接口程序
    - shell 是一个命令语言解释器（command-language interpreter）
    - bash（GNU Bourne-Again Shell）是最常用的一种shell，是当前大多数Linux发行版的默认Shell。

2. shell脚本的解释器
```
#!/bin/bash
#!/usr/bin/env bash
这样做的好处是，系统会自动在 PATH 环境变量中查找你指定的程序（本例中的 bash）
```

我是在mac中练习bash，mac默认是zsh，所以，用命令
```
chsh -s /bin/bash
```

可以查看当前的shell类型，使用
```
echo $SHELL
```
3. 模式  
Shell有交互模式和非交互模式两种
    - 简单来说，你可以将 shell 的交互模式理解为执行命令行。
    - 简单来说，你可以将 shell 的非交互模式理解为执行 shell 脚本。
  

4. 注释  
   shell 语法中，注释是特殊的语句，会被 shell 解释器忽略。
   单行注释 - 以 # 开头，到行尾结束。  
   多行注释 - 以 :<<EOF 开头，到 EOF 结束。  

5. echo AND printf  
echo与printf都可以用于输出
```
echo "hello"
echo "\"hello\""
echo "YES\nNO"  #output YES\nNO
echo -e "YES\nNO" #escape转义
:<<EOF
output:
YES
NO
EOF
```

```
echo "test" > test.txt #重定向输出文件
echo "test" >> test.txt #重定向追加文件
```

printf用于格式化输出，不会自动添加换行符
```
# 单引号
printf '%d %s\n' 1 "abc"
#  Output:1 abc

# 双引号
printf "%d %s\n" 1 "abc"
#  Output:1 abc

# 无引号
printf %s abcdef
#  Output: abcdef(并不会换行)

# 格式只指定了一个参数，但多出的参数仍然会按照该格式输出
printf "%s\n" abc def
#  Output:
#  abc
#  def

printf "%s %s %s\n" a b c d e f g h i j
#  Output:
#  a b c
#  d e f
#  g h i
#  j

# 如果没有参数，那么 %s 用 NULL 代替，%d 用 0 代替
printf "%s and %d \n"
#  Output:
#   and 0

# 格式化输出
printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg
printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234
printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543
printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876
#  Output:
#  姓名     性别   体重kg
#  郭靖     男      66.12
#  杨过     男      48.65
#  郭芙     女      47.99
```

6. 变量
   - 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
   - 中间不能有空格，可以使用下划线（_）。
   - 不能使用标点符号。
   - 不能使用 bash 里的关键字（可用 help 命令查看保留关键字）
   - 访问变量的语法形式为：${var} 和 $var 
   - 使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。
   - 使用 unset 命令可以删除变量。变量被删除后不能再次使用。unset 命令不能删除只读变量。

```
#! /bin/bash
variable="hello" #需要注意，变量赋值的等号两边不加空格
echo ${variable}
```
- 变量类型
    - 局部变量 局部变量是仅在某个脚本内部有效的变量。它们不能被其他的程序和脚本访问。
    - 环境变量 - 环境变量是对当前 shell 会话内所有的程序或脚本都可见的变量。创建它们跟创建局部变量类似，但使用的是 export 关键字，shell 脚本也可以定义环境变量。
  
|变量|描述|
|---|---| 
|$HOME|当前用户的用户目录|
|$PATH|用分号分隔的目录列表，shell 会到这些目录中查找命令|
|$PWD|当前工作目录|
|$RANDOM|0 到 32767 之间的整数|$UID|数值类型，当前用户的用户 ID|
|$PS1|主要系统输入提示符|
|$PS2|次要系统输入提示符|

7. 字符串
   



8. expr
   - expr (evaluate expressions的缩写)。"表达式求值"。Shell expr是一个功能强大。并且比较复杂的命令，它除了可以实现整数计算，还可以结合一些选项对字符串进行处理，例如计算字符串长度、字符串比较、字符串匹配、字符串提取等。
```
echo `expr 1 + 1`
echo $(expr 1 + 1) #用echo输出，，推荐第二种
#直接在交互模式
expr 1 + 1
# 注意运算符需要和数字有空格隔开
#还需 `\`转义
expr \( 10 + 10 \) \* 20
```
    - expr on MacOS不接受参数length。
    - 根据POSIX标准，使用字符串参数length、substr、index或match会产生未定义的结果。在这个版本的expr中，这些参数被视为各自的字符串值。

9. 传参
```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```
|参数处理|	说明|
|---|---|
|$#|	传递到脚本的参数个数|
|$*	|以一个单字符串显示所有向脚本传递的参数。如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。
|$$|	脚本运行的当前进程ID号 |
|$!	|后台运行的最后一个进程的ID号|
|$@	|与$*相同，但是使用时加引号，并在引号中返回每个参数。如"$@"用「"」括起来的情况、以"$1" " $2" … "$n" 的形式输出所有参数。|
|$-|	显示Shell使用的当前选项，与set命令功能相同。|
|$?|	显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。|

$* 与 $@ 区别：

- 相同点：都是引用所有参数。
- 不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，则 " * " 等价于 "1 2 3"（传递了一个参数），而 "@" 等价于 "1" "2" "3"（传递了三个参数）。

```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

echo "-- \$* 演示 ---"
for i in "$*"; do
    echo $i
done

echo "-- \$@ 演示 ---"
for i in "$@"; do
    echo $i
done


$ chmod +x test.sh 
$ ./test.sh 1 2 3
-- $* 演示 ---
1 2 3
-- $@ 演示 ---
1
2
3
```