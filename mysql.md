mysql
==========

### grammer
--------------
```
```

### example
--------------
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
