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
   