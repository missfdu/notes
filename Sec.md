## CVSS漏洞评分系统(Common Vulnerability Scoring System)

![CVSS评估系统](https://www.vulbox.com/static/web4.0/img/questionImg/leakMark3-img1.png)

## SQL注入
```php
<?php
# 包含数据库连接文件
include("config.php");
# 判断get提交的参数id是否存在
if(isset($_GET['id'])){
        $id = $_GET['id'];
    if(preg_match("/\'|\"|or|\||\-|\\\|\/|\\*|\<|\>|\^|\!|x|hex|\(|\)|\+|select/i",$id)){
            die("id error");
    }
    # 判断id的值是否大于999
    if(intval($id) > 999){
        # id 大于 999 直接退出并返回错误
        die("id error");
    }else{
        # id 小于 999 拼接sql语句
        $sql = "select * from article where id = $id order by id limit 1 ";
        echo "执行的sql为：$sql<br>";
        # 执行sql 语句
        $result = $conn->query($sql);
        # 判断有没有查询结果
        if ($result->num_rows > 0) {
            # 如果有结果，获取结果对象的值$row
            while($row = $result->fetch_assoc()) {
                echo "id: " . $row["id"]. " - title: " . $row["title"]. " <br><hr>" . $row["content"]. "<br>";
            }
        }
        # 关闭数据库连接
        $conn->close();
    }
    
}else{
    highlight_file(__FILE__);
}

?>
```

见招拆招

- `or` `select` `union` 功能关键字
  - 注释绕过
  - or == '||'
- `/*` `-` `#` 注释关键字`
- 数字型限制用位运算`~~`或进制转换`0b`绕过
- 查看过滤字符列表，尝试同义转换使SQL语句`UNION` `OR`
- 若过滤

## PHP审计

### 命令执行

`highlight_file('FILE_NAME')`

`exec('PHP_CODE;')`

`system('SH_CODE')`

显示系统文件内容

- PHP: `highlight_file()`;
- bash: `cat FILE`  `while read var\n do echo $var\n done < FILE`

过滤`.`无法字符串拼接？直接`base64_decode()`

