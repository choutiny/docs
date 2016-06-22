mysql
==========

### grammer
--------------
```

```
###address
--------------
```
http://127.0.0.1/php/dbm/
```

###寄存器的使用
----------------
```
访问:试图模式下输入:reg调出寄存器
粘帖:视图模式下输入"+p 或者其他命令粘帖
寄存器的类型:
1.无名（unnamed）寄存器：""，缓存最后一次操作内容；

2.数字（numbered）寄存器："0 ～ "9，缓存最近操作内容，复制与删除有别, "0寄存器缓存最近一次复制的内容，"1-"9缓存最近9次删除内容
7.选择及拖拽（selection and drop）寄存器："*, "+, "~，存取GUI选择文本，可用于与外部应用交互，使用前提为系统剪切板（clipboard）可用；
"ayy  就是复制当前行到 "a 字母寄存器中

 "b3yy 复制当前行和下面2行 到 “b 字母寄存器

```

show create table `table_name`;   # 显示数据库建表

create table

CREATE TABLE `clare_msg`.`user` (
    `id` INT(13) UNSIGNED NOT NULL AUTO_INCREMENT ,
    `name` VARCHAR(30) NOT NULL ,
    `email` VARCHAR(150) NULL DEFAULT NULL ,
    `passwd` INT(255) NULL DEFAULT NULL ,
PRIMARY KEY (`id`) 
)
ENGINE = InnoDB CHARACTER SET utf8 COLLATE utf8_general_ci COMMENT = '用户表';
```

###mysqli的使用方法
---------------------
```
例子一
<?php
$link = mysqli_connect("localhost", "my_user", "my_password", "world");

/* check connection */
if (mysqli_connect_errno()) {
    printf("Connect failed: %s\n", mysqli_connect_error());
    exit();
}

$query = "SELECT Name, CountryCode FROM City ORDER by ID LIMIT 3";
$result = mysqli_query($link, $query);

/* numeric array */
$row = mysqli_fetch_array($result, MYSQLI_NUM);
printf ("%s (%s)\n", $row[0], $row[1]);

/* associative array */
$row = mysqli_fetch_array($result, MYSQLI_ASSOC);
printf ("%s (%s)\n", $row["Name"], $row["CountryCode"]);

/* associative and numeric array */
$row = mysqli_fetch_array($result, MYSQLI_BOTH);
printf ("%s (%s)\n", $row[0], $row["CountryCode"]);

/* free result set */
mysqli_free_result($result);

/* close connection */
mysqli_close($link);
?>

```


```
例子二
<?php
$mysqli = new mysqli("localhost", "my_user", "my_password", "world");

/* check connection */
if ($mysqli->connect_errno) {
    printf("Connect failed: %s\n", $mysqli->connect_error);
    exit();
}

$query = "SELECT Name, CountryCode FROM City ORDER by ID LIMIT 3";
$result = $mysqli->query($query);

/* numeric array */
$row = $result->fetch_array(MYSQLI_NUM);
printf ("%s (%s)\n", $row[0], $row[1]);

/* associative array */
$row = $result->fetch_array(MYSQLI_ASSOC);
printf ("%s (%s)\n", $row["Name"], $row["CountryCode"]);

/* associative and numeric array */
$row = $result->fetch_array(MYSQLI_BOTH);
printf ("%s (%s)\n", $row[0], $row["CountryCode"]);

/* free result set */
$result->free();

/* close connection */
$mysqli->close();
?>

‵‵‵

