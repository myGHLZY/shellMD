10. 数组
    - 数组中可以存放多个值。Bash Shell 只支持一维数组（不支持多维数组），初始化时不需要定义数组大小（与 PHP 类似）。
    - 与大部分编程语言类似，数组元素的下标由 0 开始。
    - Shell 数组用括号来表示，元素用"空格"符号分割开，语法格式如下：
```
array_name=(value1 value2 ... valuen)

#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

my_array=(A B "C" D)

array_name[0]=value0
array_name[1]=value1
array_name[2]=value2
```
- 读取数组元素值的一般格式是：
```
${array_name[index]}
```
- 关联数组  
    - bash4.0后
    - Bash 支持关联数组，可以使用任意的字符串、或者整数作为下标来访问数组元素。关联数组的键是唯一的。(类似字典)关联数组使用 declare 命令来声明，语法格式如下：
```
declare -A array_name
```

- 使用 @ 或 * 可以获取数组中的所有元素，例如：
```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

my_array[0]=A
my_array[1]=B
my_array[2]=C
my_array[3]=D

echo "数组的元素为: ${my_array[*]}"
echo "数组的元素为: ${my_array[@]}"
```
- 获取数组长度的方法与获取字符串长度的方法相同，例如
```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

my_array[0]=A
my_array[1]=B
my_array[2]=C
my_array[3]=D

echo "数组元素个数为: ${#my_array[*]}"
echo "数组元素个数为: ${#my_array[@]}"
```

11. Shell 基本运算符
    - 原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。
    - expr 是一款表达式计算工具，使用它能完成表达式的求值操作。
```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

a=10
b=20

val=`expr $a + $b`
echo "a + b : $val"

val=`expr $a - $b`
echo "a - b : $val"

val=`expr $a \* $b`
echo "a * b : $val"

val=`expr $b / $a`
echo "b / a : $val"

val=`expr $b % $a`
echo "b % a : $val"

if [ $a == $b ]
then
   echo "a 等于 b"
fi
if [ $a != $b ]
then
   echo "a 不等于 b"
fi
```

|运算符|	说明|	举例|  
|---|---|---|
|+	|加法|	`expr $a + $b` 结果为 30。|
|-	|减法|	`expr $a - $b` 结果为 -10。|
|*	|乘法|	`expr $a \* $b` 结果为  200。|
|/	|除法|	`expr $b / $a` 结果为 2。|
|%	|取余|	`expr $b % $a` 结果为 0。|
|=	|赋值|	a=$b 把变量 b 的值赋给 a。|
|==	|相等|用于比较两个数字，相同则返回 true。	[ $a == $b ] 返回 false。|
|!=	|不相等|用于比较两个数字，不相同则返回 true。	[ $a != $b ] 返回 true。|
- 注意：条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b] 是错误的，必须写成 [ $a == $b ]。

- 关系运算符

|运算符|	说明|	举例|  
|---|---|---|
|-eq|	检测两个数是否相等，相等返回 true。|	[ $a -eq $b ] 返回 false。|
|-ne|	检测两个数是否不相等，不相等返回 true。|	[ $a -ne $b ] 返回 true。|
|-gt|	检测左边的数是否大于右边的，如果是，则返回 true。|	[ $a -gt $b ] 返回 false。|
|-lt|	检测左边的数是否小于右边的，如果是，则返回 true。|	[ $a -lt $b ] 返回 true。|
|-ge|	检测左边的数是否大于等于右边的，如果是，则返回 true。	|[ $a -ge $b ] 返回 false。|
|-le	检测左边的数是否小于等于右边的，如果是，则返回 true。|	[ $a -le $b ] 返回 true。|

```
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

a=10
b=20

if [ $a -eq $b ]
then
   echo "$a -eq $b : a 等于 b"
else
   echo "$a -eq $b: a 不等于 b"
fi
if [ $a -ne $b ]
then
   echo "$a -ne $b: a 不等于 b"
else
   echo "$a -ne $b : a 等于 b"
fi
if [ $a -gt $b ]
then
   echo "$a -gt $b: a 大于 b"
else
   echo "$a -gt $b: a 不大于 b"
fi
if [ $a -lt $b ]
then
   echo "$a -lt $b: a 小于 b"
else
   echo "$a -lt $b: a 不小于 b"
fi
if [ $a -ge $b ]
then
   echo "$a -ge $b: a 大于或等于 b"
else
   echo "$a -ge $b: a 小于 b"
fi
if [ $a -le $b ]
then
   echo "$a -le $b: a 小于或等于 b"
else
   echo "$a -le $b: a 大于 b"
fi
```
- 布尔运算符  
假定变量 a 为 10，变量 b 为 20

|运算符|说明|举例|
|---|---|---|
|!|	非运算，表达式为 true 则返回 false，否则返回 true。|	[ ! false ] 返回 true。|
|-o|	或运算，有一个表达式为 true 则返回 true。	|[ $a -lt 20 -o $b -gt 100 ] 返回 true。|
|-a|	与运算，两个表达式都为 true 才返回 true。|	[ $a -lt 20 -a $b -gt 100 ] 返回 false。|

- 逻辑运算符

|运算符|	说明|	举例|  
|---|---|---|
|&&|	逻辑的 AND|	[[ $a -lt 100 && $b -gt 100 ]] 返回 false|
|\|\|	|逻辑的 OR|	[[ $a -lt 100 \|\| $b -gt 100 ]] 返回 true|

- 字符串运算符

下表列出了常用的字符串运算符，假定变量 a 为 "abc"，变量 b 为 "efg"：
```
vyp 复制快捷键
```
|运算符|	说明|	举例|
|---|---|---|
|=|	检测两个字符串是否相等，相等返回 true。|	[ $a = $b ] 返回 false。|
|!=|	检测两个字符串是否不相等，不相等返回 true。	|[ $a != $b ] 返回 true。|
|-z|	检测字符串长度是否为0，为0返回 true。|	[ -z $a ] 返回 false。|
|-n|	检测字符串长度是否不为 0，不为 0 返回 true。|	[ -n "$a" ] 返回 true。|
|$|	检测字符串是否不为空，不为空返回 true。|	[ $a ] 返回 true。|

# 一定注意，变量前加 ‘$’

- 文件测试运算符

|操作符  |说明|举例| 
|----|----|----| 
|-b file|	检测文件是否是块设备文件，如果是，则返回 true。	|[ -b $file ] 返回 false。|
|-c file|	检测文件是否是字符设备文件，如果是，则返回 true。	|[ -c $file ] 返回 false。|
|-d file|	检测文件是否是目录，如果是，则返回 true。	|[ -d $file ] 返回 false。|
|-f file|	检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。	|[ -f $file ] 返回 true。|
|-g file|	检测文件是否设置了 SGID 位，如果是，则返回 true。|	[ -g $file ] 返回 false。|
|-k file|	检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。|	[ -k $file ] 返回 false。|
|-p file|	检测文件是否是有名管道，如果是，则返回 true。|	[ -p $file ] 返回 false。|
|-u file|	检测文件是否设置了 SUID 位，如果是，则返回 true。	|[ -u $file ] 返回 false。|
|-r file|	检测文件是否可读，如果是，则返回 true。|	[ -r $file ] 返回 true。|
|-w file|	检测文件是否可写，如果是，则返回 true。|	[ -w $file ] 返回 true。|
|-x file|	检测文件是否可执行，如果是，则返回 true。	|[ -x $file ] 返回 true。|
|-s file|	检测文件是否为空（文件大小是否大于0），不为空返回 true。	|[ -s $file ] 返回 true。|
|-e file|检测文件（包括目录）是否存在，如果是，则返回 true。	|[ -e $file ] 返回 true。|

- 自增和自减操作符  
let 命令允许对整数进行算术运算。
```
#!/bin/bash

# 初始化变量
num=5

# 自增
let num++

# 自减
let num--

echo $num
```
- 使用 $(( )) 进行算术运算
```
#!/bin/bash

# 初始化变量
num=5

# 自增
num=$((num + 1))

# 自减
num=$((num - 1))

echo $num
```

12. test 命令也可以简写为[]
    