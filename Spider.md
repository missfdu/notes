#   Python爬虫

## urllib模块

### urlopen

`response=urllib.request.urlopen`(*url*, *data=None*, [*timeout*, ]**)*

- 第1个参数url即请求的链接，加引号
- 第2个参数data专门给post请求携带参数
- 第3个参数timeout设置请求超时时间
- 默认GET请求，传入data则为POST请求

### Request

`req=urllib.request.Request`(*url*, *data=None*, *headers={}*, *method=None*)

- 可自定义请求头、请求方式，并封装请求信息
  - dict中是json格式的表单
  - `data=bytes(parse.urlencode(dict),'utf-8')`
- `import ssl`  `context = ssl._create_unverified_context()`
  - 使用ssl未经验证的上下文
- `response = request.urlopen(req,context=context)`

`print(response.read().decode('utf-8'))`

## request模块

```python
r = requests.get(url, headers=headers)
r = requests.post(url, data = {'key':'value'}, params=payload)
```

`r.text`返回str类型字符串
`r.json`返回解析后的dict格式结果
`r.content`

## 正则表达式

|   字符   |                             描述                             |
| :------: | :----------------------------------------------------------: |
|    \d    |         代表任意数字，就是阿拉伯数字 0-9 这些玩意。          |
|   `\D`   | 大写的就是和小写的唱反调，\d 你代表的是任意数字是吧？那么我 \D 就代表不是数字的。 |
|   `\w`   |      代表字母，数字，下划线。也就是 a-z、A-Z、0-9、_。       |
|   `\W`   |     跟 \w 唱反调，代表不是字母，不是数字，不是下划线的。     |
|    \n    |                        代表一个换行。                        |
|   `\r`   |                        代表一个回车。                        |
|   `\f`   |                          代表换页。                          |
|   `\t`   |                       代表一个 Tab 。                        |
|   `\s`   |     代表所有的空白字符，也就是上面这个：\n、\r、\t、\f。     |
|   `\S`   |            跟 \s 唱反调，代表所有不是空白的字符。            |
|   `\A`   |                      代表字符串的开始。                      |
|   `\Z`   |                      代表字符串的结束。                      |
|    ^     |                    匹配字符串开始的位置。                    |
|    $     |                    匹配字符创结束的位置。                    |
|    .     |                代表所有的单个字符，除了 \n \r                |
| `[...]`  |     代表在 [] 范围内的字符，比如 [a-z] 就代表 a到z的字母     |
| `[^...]` |          跟 [...] 唱反调，代表不在 [] 范围内的字符           |
|   {n}    | 匹配在 {n} 前面的东西，比如: o{2} 不能匹配 Bob 中的 o ，但是能匹配 food 中的两个o。 |
| `{n,m}`  | 匹配在 {n,m} 前面的东西，比如：o{1,3} 将匹配“fooooood”中的前三个o。 |
| `{n，}`  | 匹配在 {n,} 前面的东西，比如：o{2,} 不能匹配“Bob”中的“o”，但能匹配“foooood”中的所有o。 |
|   `*`    | 和 {0,} 一个样，匹配 * 前面的 0 次或多次。 比如 zo* 能匹配“z”、“zo”以及“zoo”。 |
|   `+`    | 和{1，} 一个样，匹配 + 前面 1 次或多次。 比如 zo+”能匹配“zo”以及“zoo”，但不能匹配“z”。 |
|   `？`   |          和{0,1} 一个样，匹配 ？前面 0 次或 1 次。           |
|   a\|b   |                       匹配 a 或者 b。                        |
|  `（）`  |                     匹配括号里面的内容。                     |

目标内容用`()`括起。() 实际上标记了一个子表达式的开始和结束位置，被标记的每个子表达式会依次对应每一个分组，调用 group 方法传入分组的索引即可获取提取的结果。

字符串中间尽量使用非贪婪匹配，也就是用 `.*?` 来代替 `.*`，以免出现匹配结果缺失的情况。但如果匹配的结果在字符串结尾，.*? 就有可能匹配不到任何内容了，因为它会匹配尽可能少的字符。

### re.match()方法

`re.match('正则表达式',content,re.S)`
从字符串的起始位置匹配正则表达式，如果匹配，就返回匹配成功的结果；如果不匹配，就返回 None。
绝大部分的 HTML 文本都包含了换行符，所以尽量都需要加上 re.S 修饰符。
.group()输出匹配的全部字符串
.span()输出整个字符串的长度，如(0,41)

### re.search()方法

因为 match 方法在使用时需要考虑到开头的内容，这在做匹配时并不方便。它更适合用来检测某个字符串是否符合某个正则表达式的规则。

就有另外一个search方法会依次扫描字符串，直到找到第一个符合规则的字符串，然后返回匹配内容，如果搜索完了还没有找到，就返回 None。

`re.search('正则表达式',content)`无需开头结尾，直接扫描字符串返回匹配成功的第一个结果

### re.findall()方法

`re.findall('正则表达式',content)`返回所有结果的list

### re.sub()方法

`re.sub('正则表达式','替换的值',content)`

### re.compile()方法

`pattern=re.compile('正则表达式')`

compile 还可以传入修饰符，例如 re.S 等修饰符，封装匹配模式便于下次复用

## 解析库的使用

#### XPath

| 表　达　式 | 描　　述                 |
| ---------- | ------------------------ |
| nodename   | 选取此节点的所有子节点   |
| /          | 从当前节点选取直接子节点 |
| //         | 从当前节点选取子孙节点   |
| .          | 选取当前节点             |
| ..         | 选取当前节点f的父节点    |
| @          | 选取属性                 |

```python
from lxml import etree
text = '''
<<<<<<< Updated upstream
这里是html
=======
<div>
    <ul>
         <li class="item-0"><a href="link1.html">first item</a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </ul>
 </div>
>>>>>>> Stashed changes
'''
html = etree.HTML(text)
result = etree.tostring(html)
print(result.decode('utf-8'))
```


#### BeautifulSoup
=======
首先导入 lxml 库的 etree 模块，然后声明了一段 HTML 文本，调用 HTML 类进行初始化，这样就成功构造了一个 XPath 解析对象。etree 模块可以自动修正 HTML 文本。

另外，也可以直接读取文本文件进行解析，示例如下：

```python
from lxml import etree
html = etree.parse('./test.html', etree.HTMLParser())result = etree.tostring(html)print(result.decode('utf-8'))
```

#### BeatifulSoap
>>>>>>> Stashed changes

```python
from bs4 import BeautifulSoup
soup = BeautifulSoup(html, 'lxml')
<<<<<<< Updated upstream
print(soup.prettify())
print(soup.title.string)
=======
print(soup.prettify()) # 把要解析的字符串以标准的缩进格式输出
print(soup.title.string) # 输出 HTML 中 title 节点的文本内容
>>>>>>> Stashed changes
```

## 数据存储

### 纯文本

```python
with open('explore.txt', 'a', encoding='utf-8') as file:
    file.write('\n'.join([question, author, answer]))
```

### JSON

```python
import json
# 注意JSON字符串中的数据须用双引号包围
str = '''
[{
    "name": "Bob",
    "gender": "male",
    "birthday": "1992-10-18"
}, {
    "name": "Selina",
    "gender": "female",
    "birthday": "1995-10-18"
}]
'''
print(type(str))
data = json.loads(str)
print(data)
print(type(data))
```
使用`loads()`方法将字符串转为JSON对象，结果如下。
由于最外层是中括号，所以最终的类型是列表类型。
```
<class'str'>
[{'name': 'Bob', 'gender': 'male', 'birthday': '1992-10-18'}, {'name': 'Selina', 'gender': 'female', 'birthday': '1995-10-18'}]
<class 'list'>
```

用索引来获取对应的内容,有两种方式
```python
data[0]['name']
data[0].get('name')
#推荐使用get方法，则当健名不存在时不会报错而返回None
#get方法还可传入第二个参数，键名不存在时返回该值
```

JSON转为字符串，使用`dump()`方法


```python
json.dumps(data)
json.dumps(data, indent=2) #第二个参数设置缩进
json.dumps(data, indent=2, ensure_ascii=False) #为输出中文需指定参数
```

### CSV

列表写入CSV

```python
import csv

with open('data.csv', 'w') as csvfile:
    writer = csv.writer(csvfile)
    #传入delimiter参数，可修改列与列之间的分隔符
    writer = csv.writer(csvfile, delimiter=' ')
    writer.writerow(['id', 'name', 'age'])
    writer.writerow(['10001', 'Mike', 20])
    writer.writerow(['10002', 'Bob', 22])
    writer.writerow(['10003', 'Jordan', 21])
    #参数为二维列表则写入多行
    writer.writerows([['10001', 'Mike', 20], ['10002', 'Bob', 22], ['10003', 'Jordan', 21]])
    
    #字典写入CSV
    #先定义 3 个字段，用 fieldnames 表示，然后将其传给 DictWriter 来初始化一个字典写入对象，接着可以调用 writeheader 方法先写入头信息，然后再调用 writerow 方法传入相应字典即可。
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerow({'id': '10001', 'name': 'Mike', 'age': 20})
    writer.writerow({'id': '10002', 'name': 'Bob', 'age': 22})
    writer.writerow({'id': '10003', 'name': 'Jordan', 'age': 21})
```

