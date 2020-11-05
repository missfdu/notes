# Python

### 技巧

```python
import string

def DNA_strand(dna):
    return dna.translate(string.maketrans('ATCG', 'TAGC'))
```

```python
def no_space(x):
    return "".join(x.split())
```

```python
def longest(a1, a2):
    return "".join(sorted(set(a1 + a2)))
```

###  错误

#### 正则表达式

表达式中有[花方圆]括号会和匹配规则冲突，需要转义或丢弃括号

### 语法糖

交互模式下，上一次打印出来的表达式被赋值给变量 `_`

### 字符串

原始字符串模式：在引号前加`r`就不会转义

字符串可用`*`进行重复

三重引号可跨行字符串，自动加回车，不想换行则在行尾加`\`

Py3中字符串默认以unicode存储，使用`b'字符串'`以转换为bytes方式存储

`my_str.encode('utf-8')`转换为str为bytes

`my_bytes.decode('utf-8')`转换bytes为str

### 数据结构

##### 列表List

##### 元组Tuple

##### 字典

字典转字符串时键值对用单引号，需要replace转换或者使用`json.dumps()`则为双引号

`zip(list1,list2)`将两个列表转换为字典

##### 集合