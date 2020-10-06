# PHP

### 基本语法

类似C（注释风格、每行分号结束）

```php
<?php
    //echo "Hello World!";
?>
```

### 变量

命名规则：

- 变量以 $ 符号开始，后面跟着变量的名称
- 变量名必须以字母或者下划线字符开始
- 变量名只能包含字母数字字符以及下划线（A-z、0-9 和 _ ）
- 变量名不能包含空格
- 变量名是区分大小写的

PHP是**弱类型语言**

PHP 有四种不同的**变量作用域**(脚本中变量可被引用/使用的部分)：

- local
- global
  - 在所有函数外部定义的变量，拥有全局作用域
  - 要在一个函数中访问一个全局变量，需要使用 global 关键字
  - 所有全局变量存储在一个名为 $GLOBALS[*index*] 的数组中。 *index* 保存变量的名称。这个数组可以在函数内部访问，也可以直接用来更新全局变量。
- static
  - 当函数完成时，它的所有变量通常都会被删除,但有时希望某个局部变量不要被删除
  - 第一次声明变量时使用 **static** 关键字，则每次调用该函数时，该变量将会保留着函数前一次被调用时的值
- parameter

### 输出

echo 和 print 区别:

- echo - 可以输出一个或多个字符串，无返回值。速度比print快
- print - 只允许输出一个字符串，返回值总为 1
- echo和print都是语言结构，括号()加不加均可

```php
$cars=array("Volvo","BMW","Toyota");
echo "这是一个", "字符串，", "使用了", "多个", "参数。";
echo "我车的品牌是 {$cars[0]}";print "Hello world!<br>";
```

### PHP EOF(heredoc)

PHP EOF(heredoc)是一种在命令行shell（如sh、csh、ksh、bash、PowerShell和zsh）和程序语言（像Perl、PHP、Python和Ruby）里定义一个字符串的方法。

使用概述：

1. 必须后接分号，否则编译通不过。
2. **EOF** 可以用任意其它字符代替，只需保证结束标识与开始标识一致。
3. **结束标识必须顶格独自占一行**(即必须从行首开始，前后不能衔接任何空白和字符)。
4. 开始标识可以不带引号或带单双引号，不带引号与带双引号效果一致，解释内嵌的变量和转义符号，带单引号则不解释内嵌的变量和转义符号。
5. 当内容需要内嵌引号（单引号或双引号）时，不需要加转义符，本身对单双引号转义，此处相当与q和qq的用法。