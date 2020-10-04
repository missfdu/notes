# HTML基础
### 元素  
```html
<p>content</p>//Paragraph Element  
<p class="editor-note">XX</p>//With Attribute
```
![img](https://mdn.mozillademos.org/files/16475/element.png)

##### 块级元素和内联元素

* 块级元素在页面中以块的形式展现 —— 相对于其前面的内容它会出现在**新的一行**，其后的内容也会被挤到下一行展现。块级元素通常用于展示页面上**结构化的内容**，例如段落、列表、导航菜单、页脚等等。一个以block形式展现的块级元素不会被嵌套进内联元素中，但可以嵌套在其它块级元素中，例如`<p>`。
* 内联元素通常**出现在块级元素中**并环绕文档内容的一小部分，而不是一整个段落或者一组内容。内联元素**不会导致文本换行**：它通常出现在一堆文字之间，例如超链接元素[`<a>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a)或者强调元素[`<em>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/em)和 [`<strong>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/strong)

##### 图像

```html
<img src="images/firefox-icon.png" alt="测试图片">
```
* `src`=地址属性
* `alt`=替换文字属性，图像不可用时显示

##### 链接

```html
<a href="https://www.mozilla.org/zh-CN/about/manifesto/">Mozilla 宣言</a>
<a href="https://www.mozilla.org/en-US/">
  <img src="mozilla-image.png" alt="mozilla logo that links to the mozilla homepage">
</a><!--块级链接之图像元素-->
```

* `<a>`元素，(abbrev. anchor锚)
* `href`属性=**h**ypertext **ref**erence
* `title`属性=为链接声明额外的信息，鼠标悬停显示
* `target`属性=指定链接如何呈现，`target="_blank"`新标签页中
* `download`属性=默认保存文件名
* 相对URL更简洁高效，../表示上一级

### 属性

* 属性值需用引号(单双均可)包围，防止空格等使解析错误

* **布尔属性**:没有值的属性，属性值和属性名一样

  ```html
  <!-- 使用disabled属性来防止终端用户输入文本到输入框中 -->
  <input type="text" disabled="disabled">
  <input type="text" disabled>
  <!--以上两种写法等价-->
  ```

### 文字排版

* 标题Heading，6个级别

  ```html
  <h1>主标题</h1>
  <h2>顶层标题</h2>
  <h3>子标题</h3>
  <h4>次子标题</h4>
  ```
  
* 列表List

  * `<ul>`无序列表Unordered List
  * `<ol>`有序列表Ordered List
  * 列表的每个项目用一个列表项目(List Item)元素` <li>` 包围，可嵌套

  ```html
  <p>Mozilla 是一个全球社区，这里聚集着来自五湖四海的</p> 
  <ul> 
    <li>技术人员</li>
      <ul>
          <li>前端</li>
          <li>后端</li>
      </ul>
    <li>思考者</li>
    <li>建造者</li>义元素
  
  `<b>`粗体，`<i>`斜体，`<u>`下划线
  ```

* 描述列表`<dl>`Description List

  * `<dt>`描述术语Description Term

  * `<dd>`描述部分Description Description

    ```html
    <dl>
      <dt>培根</dt>
        <dd>整个世界的粘合剂。</dd>
      <dt>咖啡</dt>
        <dd>一种浅棕色的饮料。</dd>
        <dd>可以在清晨带来活力。</dd>
    </dl>
    ```

* 块引用`<blockquote>`

  ```html
  <blockquote cite="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote">
    <p>The <strong>HTML <code>&lt;blockquote&gt;</code> Element</strong> (or <em>HTML Block
    Quotation Element</em>) indicates that the enclosed text is an extended quotation.</p>
  </blockquote>
  ```

  浏览器在渲染块引用时默认会增加缩进，作为引用的一个指示符

* 行内引用`<q>`

  ```html
  <p>The quote element — <code>&lt;q&gt;</code> — is <q cite="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/q">intended
  for short quotations that don't require paragraph breaks.</q></p>
  ```

  浏览器默认将其作为普通文本放入引号内

* `<cite>`元素

  ```html
  <a href="http://www.brainyquote.com/quotes/authors/c/confucius.html"><cite>孔子</cite></a>曰：</p>
  <blockquote cite="https://zh.wikipedia.org/zh-hans/孔子">
    <p>譬如为山，未成一篑，止，吾止也。譬如平地，虽覆一篑，进，吾往也。</p>
  </blockquote>
  ```

  浏览器不会显示`cite`属性的内容。使用`<cite>`元素能确保引用来源可显示

* 缩略语`<abbr>`

  ```html
  <p>我们使用 <abbr title="超文本标记语言（Hypertext Markup Language）">HTML</abbr> 来组织网页文档。</p>
  ```

  title属性值在光标悬停时显示

* 下标`<sub>`，上标`<sup>`

* [`<code>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/code): 用于标记计算机通用代码。

* [`<pre>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/pre): 用于保留空白字符（通常用于代码块）——如果您在文本中使用缩进或多余的空白，浏览器将忽略它，您将不会在呈现的页面上看到它。但是，如果您将文本包含在`<pre></pre>`标签中，那么空白将会以与你在文本编辑器中看到的相同的方式渲染出来。

* [`<var>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/var): 用于标记具体变量名。

* [`<kbd>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/kbd): 用于标记输入电脑的键盘（或其他类型）输入。

* [`<samp>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/samp): 用于标记计算机程序的输出。

##### 实体引用—包含特殊字符

| 原义字符 | 等价字符引用 |
| :------- | :----------- |
| <        | `&lt;`       |
| >        | `&gt;`       |
| "        | `&quot;`     |
| '        | `&apos;`     |
| &        | `&amp;`      |



### HTML文档

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>测试页面</title>
  </head>
  <body>
    <img src="images/firefox-icon.png" alt="测试图片">
  </body>
</html>
```

##### 整体结构

* `<!DOCTYPE html>` :声明文档类型，仅用于保证文档正常读取
* `<html></html>` : [`<html>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/html)元素，包含整个页面的内容，是根元素
  * `<html lang="en-US">`lang属性指定语言
* `<head></head>`: `<head>元素`是一个容器
  * `<meta>`:元数据元素
    * `<meta charset="utf-8">`指定文档使用 UTF-8 字符编码
    * `<meta name="author" content="syzedu">`指定作者
    * `<meta name="description" content="A personal website">`指定页面简介
  * `<title></title>` — [`<title>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/title) 元素，设置页面的标题
  * `<link>`元素
    * `<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">`指定页面图标
    * `<link rel="stylesheet" href="style.css">`指定CSS样式表
* `<body></body>` — [`<body>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/body) 元素。该元素包含期望让用户在访问页面时看到的内容
- [`<header>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/header)：页眉。
  - [`<nav>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/nav)：导航栏。
  - [`<main>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/main)：主内容。主内容中还可以有各种子内容区段，可用[`<article>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/article)、[`<section>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/section) 和 [`<div>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div) 等元素表示。
  - [`<aside>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/aside)：侧边栏，经常嵌套在 [`<main>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/main) 中。
  - [`<footer>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/footer)：页脚。

##### 布局元素细节

- [`<main>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/main) 存放每个页面独有的内容。每个页面上只能用一次 `<main>`，且直接位于 [`<body>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/body) 中。最好不要把它嵌套进其它元素。
- [`<article>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/article) 包围的内容即一篇文章，与页面其它部分无关（比如一篇博文）。
- [`<section>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/section) 与 `<article>` 类似，但 `<section>` 更适用于组织页面使其按功能（比如迷你地图、一组文章标题和摘要）分块。一般的最佳用法是：以 [标题](https://developer.mozilla.org/en-US/Learn/HTML/Howto/Set_up_a_proper_title_hierarchy) 作为开头；也可以把一篇 `<article>` 分成若干部分并分别置于不同的 `<section>` 中，也可以把一个区段 `<section>` 分成若干部分并分别置于不同的 `<article>` 中，取决于上下文。
- [`<aside>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/aside) 包含一些间接信息（术语条目、作者简介、相关链接，等等）。
- [`<header>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/header) 是简介形式的内容。如果它是 [`<body>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/body) 的子元素，那么就是网站的全局页眉。如果它是 [`<article>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/article) 或[`<section>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/section) 的子元素，那么它是这些部分特有的页眉（此 `<header>` 非彼 [标题](https://developer.mozilla.org/zh-CN/docs/learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML#增加一个标题)）。
- [`<nav>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/nav) 包含页面主导航功能。其中不应包含二级链接等内容。
- [`<footer>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/footer) 包含了页面的页脚部分。

##### 无语义元素

只想将一组元素作为一个单独的实体来修饰来响应单一的用 [CSS](https://developer.mozilla.org/zh-CN/docs/Glossary/CSS) 或 [JavaScript](https://developer.mozilla.org/zh-CN/docs/Glossary/JavaScript)

* [`<span>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/span) 是一个内联的（inline）无语义元素，最好只用于无法找到更好的语义元素来包含内容时

* [`<div>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div) 是一个块级无语义元素，应仅用于找不到更好的块级元素时

  > `<div>` 非常便利但容易被滥用。由于它们没有语义值，会使 HTML 代码变得混乱。要小心使用，只有在没有更好的语义方案时才选择它

##### 换行`<br>`和水平分割线`<hr>`

# 多媒体与嵌入

# HTML表格

定义：表格是由行和列组成的结构化数据集(表格数据)

表格的工作方法：在行和列的标题之间进行视觉关联，让信息能够很简单地被解读出来。

基本框架  

```html
<table>
  <tr>
    <th scope="row">table header,作为行标题的单元格</th>
      <!--scope属性可选"row","col","rowgroup","colgroup"-->
    <td>table data,作为数据的单元格</td>
  </tr>
</table>
```

跨行列单元格  
单元格属性`colspan="2"`,`rowspan="3"`

整列样式  
在`<table>`标签下面插入元素`<colgroup>`

```html
<colgroup>
    <col>
    <col span="2">
    <col style="background-color:#DCC48E; border:4px solid #C1437A;">
    <col span="2" style="width:42px;">
</colgroup>
```

表格标题元素`<caption>`

表格结构`<thead>`,`<tbody>`,`<tfoot>`

表格可以嵌套，但可读性较差，如下在`<tr>`中嵌套表格  

```html
<tr>
    <td id="nested">
      <table id="table2">
        <tr>
          <td>cell1</td>
          <td>cell2</td>
        </tr>
      </table>
    </td>
    <td>cell2</td>
    <td>cell3</td>
</tr>
```

