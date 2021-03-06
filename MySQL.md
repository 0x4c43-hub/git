<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [apt-get install mysql-server //服务器](#apt-get-install-mysql-server-%E6%9C%8D%E5%8A%A1%E5%99%A8)
  - [apt-get install mysql-client //客服端](#apt-get-install-mysql-client-%E5%AE%A2%E6%9C%8D%E7%AB%AF)
  - [apt-get install libmysqlclient-dev //库](#apt-get-install-libmysqlclient-dev-%E5%BA%93)
  - [编译时链接 -lmysqlclient](#%E7%BC%96%E8%AF%91%E6%97%B6%E9%93%BE%E6%8E%A5--lmysqlclient)
  - [sudo service mysql start //开启服务](#sudo-service-mysql-start-%E5%BC%80%E5%90%AF%E6%9C%8D%E5%8A%A1)
  - [sudo service mysql stop //停止服务](#sudo-service-mysql-stop-%E5%81%9C%E6%AD%A2%E6%9C%8D%E5%8A%A1)
  - [sudo service mysql status //服务状态](#sudo-service-mysql-status-%E6%9C%8D%E5%8A%A1%E7%8A%B6%E6%80%81)
  - [sudo service mysql restart //重启服务](#sudo-service-mysql-restart-%E9%87%8D%E5%90%AF%E6%9C%8D%E5%8A%A1)
  - [sudo vi /etc/mysql/debian.cnf](#sudo-vi-etcmysqldebiancnf)
  - [mysql -udebian-sys-maint -p](#mysql--udebian-sys-maint--p)
  - [use mysql //打开mysql数据库](#use-mysql-%E6%89%93%E5%BC%80mysql%E6%95%B0%E6%8D%AE%E5%BA%93)
  - [update user set authentication_string=SHA1/MD5('new password') where user='root' and Host='localhost'; //设置root用户密码,mysql 8移除了PASSWORD函数，可使用SHA1或者MD5](#update-user-set-authentication_stringsha1md5new-password-where-userroot-and-hostlocalhost-%E8%AE%BE%E7%BD%AEroot%E7%94%A8%E6%88%B7%E5%AF%86%E7%A0%81mysql-8%E7%A7%BB%E9%99%A4%E4%BA%86password%E5%87%BD%E6%95%B0%E5%8F%AF%E4%BD%BF%E7%94%A8sha1%E6%88%96%E8%80%85md5)
  - [select user,authenticatian_string from user; //查看用户和密码](#select-userauthenticatian_string-from-user-%E6%9F%A5%E7%9C%8B%E7%94%A8%E6%88%B7%E5%92%8C%E5%AF%86%E7%A0%81)
  - [update user set plugin="mysql_native_password";](#update-user-set-pluginmysql_native_password)
  - [flush privileges; //刷新权限配置](#flush-privileges-%E5%88%B7%E6%96%B0%E6%9D%83%E9%99%90%E9%85%8D%E7%BD%AE)
  - [sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf](#sudo-vi-etcmysqlmysqlconfdmysqldcnf)
  - [CREATE USER <用户名>@<主机名> IDENTIFIED BY SHA1/MD5('password'); //创建用户](#create-user-%E7%94%A8%E6%88%B7%E5%90%8D%E4%B8%BB%E6%9C%BA%E5%90%8D-identified-by-sha1md5password-%E5%88%9B%E5%BB%BA%E7%94%A8%E6%88%B7)
  - [GRANT privileges/ALL ON databasename.tablename TO 'username'@'host; //授权](#grant-privilegesall-on-databasenametablename-to-usernamehost-%E6%8E%88%E6%9D%83)
  - [GRANT privileges ON databasename.tablename TO 'username'@'host WITH GRANT OPTION;](#grant-privileges-on-databasenametablename-to-usernamehost-with-grant-option)
  - [SET PASSWORD FOR 'username'@'host'=PASSWORD('password'); //设置用户密码](#set-password-for-usernamehostpasswordpassword-%E8%AE%BE%E7%BD%AE%E7%94%A8%E6%88%B7%E5%AF%86%E7%A0%81)
  - [SET PASSWORD=PASSWORD('password');//设置当前用户密码](#set-passwordpasswordpassword%E8%AE%BE%E7%BD%AE%E5%BD%93%E5%89%8D%E7%94%A8%E6%88%B7%E5%AF%86%E7%A0%81)
  - [REVOKE privileges ON databasename.tablename FROM 'username'@'host;](#revoke-privileges-on-databasenametablename-from-usernamehost)
  - [DROP USER 'username'@'host'; //删除用户](#drop-user-usernamehost-%E5%88%A0%E9%99%A4%E7%94%A8%E6%88%B7)
- [show databases [like '数据库名']; // 查看当前用户权限范围内的数据库](#show-databases-like-%E6%95%B0%E6%8D%AE%E5%BA%93%E5%90%8D--%E6%9F%A5%E7%9C%8B%E5%BD%93%E5%89%8D%E7%94%A8%E6%88%B7%E6%9D%83%E9%99%90%E8%8C%83%E5%9B%B4%E5%86%85%E7%9A%84%E6%95%B0%E6%8D%AE%E5%BA%93)
- [show tables [like '数据表名']; // 查看当前用户权限范围内的数据表](#show-tables-like-%E6%95%B0%E6%8D%AE%E8%A1%A8%E5%90%8D--%E6%9F%A5%E7%9C%8B%E5%BD%93%E5%89%8D%E7%94%A8%E6%88%B7%E6%9D%83%E9%99%90%E8%8C%83%E5%9B%B4%E5%86%85%E7%9A%84%E6%95%B0%E6%8D%AE%E8%A1%A8)
- [MySQL 创建数据库](#mysql-%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93)
- [drop 命令删除数据库](#drop-%E5%91%BD%E4%BB%A4%E5%88%A0%E9%99%A4%E6%95%B0%E6%8D%AE%E5%BA%93)
- [MySQL 选择数据库](#mysql-%E9%80%89%E6%8B%A9%E6%95%B0%E6%8D%AE%E5%BA%93)
- [MySQL 数据类型](#mysql-%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
- [日期和时间类型](#%E6%97%A5%E6%9C%9F%E5%92%8C%E6%97%B6%E9%97%B4%E7%B1%BB%E5%9E%8B)
- [字符串类型](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%B1%BB%E5%9E%8B)
- [MySQL 创建数据表](#mysql-%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E8%A1%A8)
- [以下例子中我们将在 RUNOOB 数据库中创建数据表runoob_tbl：](#%E4%BB%A5%E4%B8%8B%E4%BE%8B%E5%AD%90%E4%B8%AD%E6%88%91%E4%BB%AC%E5%B0%86%E5%9C%A8-runoob-%E6%95%B0%E6%8D%AE%E5%BA%93%E4%B8%AD%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E8%A1%A8runoob_tbl)
- [MySQL 删除数据表](#mysql-%E5%88%A0%E9%99%A4%E6%95%B0%E6%8D%AE%E8%A1%A8)
- [MySQL 插入数据](#mysql-%E6%8F%92%E5%85%A5%E6%95%B0%E6%8D%AE)
- [MySQL 查询数据](#mysql-%E6%9F%A5%E8%AF%A2%E6%95%B0%E6%8D%AE)
- [MySQL WHERE 子句](#mysql-where-%E5%AD%90%E5%8F%A5)
- [MySQL UPDATE 更新](#mysql-update-%E6%9B%B4%E6%96%B0)
- [MySQL DELETE 语句](#mysql-delete-%E8%AF%AD%E5%8F%A5)
- [MySQL LIKE 子句](#mysql-like-%E5%AD%90%E5%8F%A5)
- [MySQL UNION 操作符](#mysql-union-%E6%93%8D%E4%BD%9C%E7%AC%A6)
  - [参数](#%E5%8F%82%E6%95%B0)
- [MySQL 排序](#mysql-%E6%8E%92%E5%BA%8F)
- [MySQL GROUP BY 语句](#mysql-group-by-%E8%AF%AD%E5%8F%A5)
- [使用 WITH ROLLUP](#%E4%BD%BF%E7%94%A8-with-rollup)
- [MySQL 连接的使用](#mysql-%E8%BF%9E%E6%8E%A5%E7%9A%84%E4%BD%BF%E7%94%A8)
- [MySQL NULL 值处理](#mysql-null-%E5%80%BC%E5%A4%84%E7%90%86)
- [MySQL 正则表达式](#mysql-%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)
- [MySQL 事务](#mysql-%E4%BA%8B%E5%8A%A1)
- [事务控制语句：](#%E4%BA%8B%E5%8A%A1%E6%8E%A7%E5%88%B6%E8%AF%AD%E5%8F%A5)
- [MySQL ALTER命令](#mysql-alter%E5%91%BD%E4%BB%A4)
  - [删除，添加或修改表字段](#%E5%88%A0%E9%99%A4%E6%B7%BB%E5%8A%A0%E6%88%96%E4%BF%AE%E6%94%B9%E8%A1%A8%E5%AD%97%E6%AE%B5)
  - [修改字段类型及名称](#%E4%BF%AE%E6%94%B9%E5%AD%97%E6%AE%B5%E7%B1%BB%E5%9E%8B%E5%8F%8A%E5%90%8D%E7%A7%B0)
  - [ALTER TABLE 对 Null 值和默认值的影响](#alter-table-%E5%AF%B9-null-%E5%80%BC%E5%92%8C%E9%BB%98%E8%AE%A4%E5%80%BC%E7%9A%84%E5%BD%B1%E5%93%8D)
  - [修改字段默认值](#%E4%BF%AE%E6%94%B9%E5%AD%97%E6%AE%B5%E9%BB%98%E8%AE%A4%E5%80%BC)
  - [修改表名](#%E4%BF%AE%E6%94%B9%E8%A1%A8%E5%90%8D)
- [MySQL 索引](#mysql-%E7%B4%A2%E5%BC%95)
  - [普通索引  //无任何限制](#%E6%99%AE%E9%80%9A%E7%B4%A2%E5%BC%95--%E6%97%A0%E4%BB%BB%E4%BD%95%E9%99%90%E5%88%B6)
  - [唯一索引  //索引列的值必须唯一，但允许有空值](#%E5%94%AF%E4%B8%80%E7%B4%A2%E5%BC%95--%E7%B4%A2%E5%BC%95%E5%88%97%E7%9A%84%E5%80%BC%E5%BF%85%E9%A1%BB%E5%94%AF%E4%B8%80%E4%BD%86%E5%85%81%E8%AE%B8%E6%9C%89%E7%A9%BA%E5%80%BC)
- [使用ALTER 命令添加和删除索引](#%E4%BD%BF%E7%94%A8alter-%E5%91%BD%E4%BB%A4%E6%B7%BB%E5%8A%A0%E5%92%8C%E5%88%A0%E9%99%A4%E7%B4%A2%E5%BC%95)
- [使用 ALTER 命令添加和删除主键](#%E4%BD%BF%E7%94%A8-alter-%E5%91%BD%E4%BB%A4%E6%B7%BB%E5%8A%A0%E5%92%8C%E5%88%A0%E9%99%A4%E4%B8%BB%E9%94%AE)
- [显示索引信息](#%E6%98%BE%E7%A4%BA%E7%B4%A2%E5%BC%95%E4%BF%A1%E6%81%AF)
- [MySQL 临时表](#mysql-%E4%B8%B4%E6%97%B6%E8%A1%A8)
- [删除MySQL 临时表](#%E5%88%A0%E9%99%A4mysql-%E4%B8%B4%E6%97%B6%E8%A1%A8)
- [MySQL 复制表](#mysql-%E5%A4%8D%E5%88%B6%E8%A1%A8)
  - [第一种方法](#%E7%AC%AC%E4%B8%80%E7%A7%8D%E6%96%B9%E6%B3%95)
  - [第二种方法](#%E7%AC%AC%E4%BA%8C%E7%A7%8D%E6%96%B9%E6%B3%95)
- [MySQL元数据](#mysql%E5%85%83%E6%95%B0%E6%8D%AE)
- [MySQL 序列使用](#mysql-%E5%BA%8F%E5%88%97%E4%BD%BF%E7%94%A8)
  - [使用 AUTO_INCREMENT](#%E4%BD%BF%E7%94%A8-auto_increment)
  - [获取AUTO_INCREMENT值](#%E8%8E%B7%E5%8F%96auto_increment%E5%80%BC)
  - [重置序列](#%E9%87%8D%E7%BD%AE%E5%BA%8F%E5%88%97)
  - [设置序列的开始值](#%E8%AE%BE%E7%BD%AE%E5%BA%8F%E5%88%97%E7%9A%84%E5%BC%80%E5%A7%8B%E5%80%BC)
- [MySQL 处理重复数据](#mysql-%E5%A4%84%E7%90%86%E9%87%8D%E5%A4%8D%E6%95%B0%E6%8D%AE)
  - [防止表中出现重复数据](#%E9%98%B2%E6%AD%A2%E8%A1%A8%E4%B8%AD%E5%87%BA%E7%8E%B0%E9%87%8D%E5%A4%8D%E6%95%B0%E6%8D%AE)
  - [统计重复数据](#%E7%BB%9F%E8%AE%A1%E9%87%8D%E5%A4%8D%E6%95%B0%E6%8D%AE)
  - [过滤重复数据](#%E8%BF%87%E6%BB%A4%E9%87%8D%E5%A4%8D%E6%95%B0%E6%8D%AE)
  - [删除重复数据](#%E5%88%A0%E9%99%A4%E9%87%8D%E5%A4%8D%E6%95%B0%E6%8D%AE)
- [MySQL 及 SQL 注入](#mysql-%E5%8F%8A-sql-%E6%B3%A8%E5%85%A5)
- [MySQL 导出数据](#mysql-%E5%AF%BC%E5%87%BA%E6%95%B0%E6%8D%AE)
  - [使用 SELECT ... INTO OUTFILE 语句导出数据](#%E4%BD%BF%E7%94%A8-select--into-outfile-%E8%AF%AD%E5%8F%A5%E5%AF%BC%E5%87%BA%E6%95%B0%E6%8D%AE)
- [MySQL 导入数据](#mysql-%E5%AF%BC%E5%85%A5%E6%95%B0%E6%8D%AE)
- [mysqlimport的常用选项介绍](#mysqlimport%E7%9A%84%E5%B8%B8%E7%94%A8%E9%80%89%E9%A1%B9%E4%BB%8B%E7%BB%8D)
- [MySQL 函数](#mysql-%E5%87%BD%E6%95%B0)
- [MySQL 运算符](#mysql-%E8%BF%90%E7%AE%97%E7%AC%A6)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

[MySQL教程](https://www.runoob.com/mysql/)
#### apt-get install mysql-server //服务器
#### apt-get install mysql-client //客服端
#### apt-get install libmysqlclient-dev //库
#### 编译时链接 -lmysqlclient
sudo mysql_secure_installation
#### sudo service mysql start //开启服务
#### sudo service mysql stop //停止服务
#### sudo service mysql status //服务状态
#### sudo service mysql restart //重启服务
#### sudo vi /etc/mysql/debian.cnf
#### mysql -udebian-sys-maint -p
#### use mysql //打开mysql数据库
#### update user set authentication_string=SHA1/MD5('new password') where user='root' and Host='localhost'; //设置root用户密码,mysql 8移除了PASSWORD函数，可使用SHA1或者MD5
#### select user,authentication_string from user; //查看用户和密码
#### update user set plugin="mysql_native_password";
#### flush privileges; //刷新权限配置
#### sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
最后一行加入skip-grant-tables //跳过权限验证
#### CREATE USER <用户名>@<主机名> IDENTIFIED BY SHA1/MD5('password'); //创建用户
#### GRANT privileges/ALL ON databasename.tablename TO 'username'@'host; //授权   
以上授权用户不能给其他用户授权,可使用下面的命令
#### GRANT privileges ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
#### SET PASSWORD FOR 'username'@'host'=PASSWORD('password'); //设置用户密码
#### SET PASSWORD=PASSWORD('password');//设置当前用户密码
#### REVOKE privileges ON databasename.tablename FROM 'username'@'host;
#### DROP USER 'username'@'host'; //删除用户

### show databases [like '数据库名']; // 查看当前用户权限范围内的数据库
### show tables [like '数据表名']; // 查看当前用户权限范围内的数据表
### MySQL 创建数据库
* CREATE DATABASE 数据库名;
* mysqladmin -u root -p create RUNOOB
### drop 命令删除数据库
* drop database <数据库名>;
* mysqladmin -u root -p drop RUNOOB
### MySQL 选择数据库
* use RUNOOB;
### MySQL 数据类型
|类型|	大小|	范围（有符号）|	范围（无符号）|	用途|
|---|---|---|---|---|
|TINYINT|	1 byte|	(-128，127)|	(0，255)|	小整数值|
|SMALLINT|	2 bytes|	(-32 768，32 767)|	(0，65 535)|	大整数值|
|MEDIUMINT|	3 bytes|	(-8 388 608，8 388 607)|	(0，16 777 215)|	大整数值|
|INT或INTEGER|	4 bytes|	(-2 147 483 648，2 147 483 647)|	(0，4 294 967 295)|	大整数值|
|BIGINT|	8 bytes|	(-9,223,372,036,854,775,808，9 223 372 036 854 775 807)|	(0，18 446 744 073 709 551 615)	|极大整数值|
|FLOAT|	4 bytes|(-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38)|	0，(1.175 494 351 E-38，3.402 823 466 E+38)	|单精度浮点数值|
|DOUBLE|	8 bytes|	(-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308)|	0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308)|	双精度浮点数值|
|DECIMAL|	对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2	|依赖于M和D的值	|依赖于M和D的值	|小数值|
### 日期和时间类型
|类型|	大小( bytes)|	范围|	格式|	用途 |
| ---|---|---|---|---|
|DATE	|3|	1000-01-01/9999-12-31|	YYYY-MM-DD	|日期值|
|TIME	|3	|'-838:59:59'/'838:59:59'|	HH:MM:SS	|时间值或持续时间|
|YEAR	|1|	1901/2155	|YYYY	|年份值|
|DATETIME|	8|	1000-01-01 00:00:00/9999-12-31 23:59:59|	YYYY-MM-DD HH:MM:SS|	混合日期和时间值|
|TIMESTAMP|	4|	1970-01-01 00:00:00/2038结束时间是第 2147483647 秒，北京时间 2038-1-19 11:14:07，格林尼治时间 2038年1月19日 凌晨 03:14:07|YYYYMMDD HHMMSS	|混合日期和时间值，时间戳|
### 字符串类型
|类型|	大小|	用途|
|---|---|---|
|CHAR	|0-255bytes	|定长字符串|
|VARCHAR|	0-65535bytes|	变长字符串|
|TINYBLOB|	0-255bytes|	不超过 255 个字符的二进制字符串|
|TINYTEXT	|0-255bytes|	短文本字符串|
|BLOB	|0-65 535bytes|	二进制形式的长文本数据|
|TEXT	|0-65 535bytes|	长文本数据|
|MEDIUMBLOB|	0-16777 215 bytes|	二进制形式的中等长度文本数据|
|MEDIUMTEXT|	0-16777 215 bytes	|中等长度文本数据|
|LONGBLOB	|0-4 294967 295 bytes	|二进制形式的极大文本数据|
|LONGTEXT	|0-4 294967 295 bytes	|极大文本数据|
### MySQL 创建数据表
* CREATE TABLE table_name (column_name column_type);
* SHOW COLUMNS FROM table_name;
### 以下例子中我们将在 RUNOOB 数据库中创建数据表runoob_tbl：

    CREATE TABLE IF NOT EXISTS runoob_tbl(
       runoob_id INT UNSIGNED AUTO_INCREMENT,
       runoob_title VARCHAR(100) NOT NULL,
       runoob_author VARCHAR(40) NOT NULL,
       submission_date DATE,
       PRIMARY KEY ( runoob_id )
    )ENGINE=InnoDB DEFAULT CHARSET=utf8;
>实例解析：
>>* 如果你不想字段为 NULL 可以设置字段的属性为 NOT NULL， 在操作数据库时如果输入该字段的数据为NULL ，就会报错。
>>* AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。
>>* PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。
>>* ENGINE 设置存储引擎，CHARSET 设置编码。
#### AUTO_INCREMENT说明：

1.如果把一个NULL插入到一个AUTO_INCREMENT数据列里去，MySQL将自动生成下一个序列编号。编号从1开始，并1为基数递增。

2.把0插入AUTO_INCREMENT数据列的效果与插入NULL值一样。但不建议这样做，还是以插入NULL值为好。

3.当插入记录时，没有为AUTO_INCREMENT明确指定值，则等同插入NULL值。

4.当插入记录时，如果为AUTO_INCREMENT数据列明确指定了一个数值，则会出现两种情况，情况一，如果插入的值与已有的编号重复，则会出现出错信息，因为AUTO_INCREMENT数据列的值必须是唯一的；情况二，如果插入的值大于已编号的值，则会把该插入到数据列中，并使在下一个编号将从这个新值开始递增。也就是说，可以跳过一些编号。

5.AUTO_INCREMENT_INCREMEN设置起始值，AUTO_INCREMENT_OFFICE设置增幅。

### 查看表结构
* desc tablename;
* describe tablename;
* show create table tablename;
* show fields from tablename;
* show full fields from tablename;
* show columns from tablename;
* show table status like '%tablename%' \G;
### MySQL 删除数据表
* DROP TABLE table_name ;

### MySQL 插入数据
* INSERT INTO table_name( field1, field2,...fieldN ) VALUES( value1, value2,...valueN );
* INSERT INTO table_name VALUES( value1, value2,...valueN );
### MySQL 查询数据
SELECT column_name,column_name FROM table_name [WHERE Clause] [LIMIT N][ OFFSET M];

    查询语句中你可以使用一个或者多个表，表之间使用逗号(,)分割，并使用WHERE语句来设定查询条件。
    SELECT 命令可以读取一条或者多条记录。
    你可以使用星号（*）来代替其他字段，SELECT语句会返回表的所有字段数据
    你可以使用 WHERE 语句来包含任何条件。
    你可以使用 LIMIT 属性来设定返回的记录数。
    你可以通过OFFSET指定SELECT语句开始查询的数据偏移量。默认情况下偏移量为0。
*********************
### MySQL WHERE 子句
SELECT field1, field2,...fieldN FROM table_name1, table_name2... [WHERE condition1 [AND [OR]] condition2.....;
### MySQL UPDATE 更新
UPDATE table_name SET field1=new-value1, field2=new-value2 [WHERE Clause];

### MySQL DELETE 语句
DELETE FROM table_name [WHERE Clause];
### MySQL LIKE 子句
SELECT field1, field2,...fieldN FROM table_name WHERE field1 LIKE condition1 [AND [OR]] filed2 = 'somevalue';
### MySQL UNION 操作符
    SELECT expression1, expression2, ... expression_n FROM tables [WHERE conditions]
    UNION [ALL | DISTINCT]
    SELECT expression1, expression2, ... expression_n FROM tables [WHERE conditions];
#### 参数
* expression1, expression2, ... expression_n: 要检索的列。
* tables: 要检索的数据表。
* WHERE conditions: 可选， 检索条件。
* DISTINCT: 可选，删除结果集中重复的数据。默认情况下 UNION 操作符已经删除了重复数据，所以 DISTINCT 修饰符对结果没啥影响。
* ALL: 可选，返回所有结果集，包含重复数据。

### MySQL 排序
SELECT field1, field2,...fieldN FROM table_name1, table_name2... [WHERE conditions] ORDER BY field1 [ASC][DESC][默认 ASC]], [field2...] [ASC [DESC][默认 ASC]];
### MySQL GROUP BY 语句
* GROUP BY 语句根据一个或多个列对结果集进行分组。
* 在分组的列上我们可以使用 COUNT, SUM, AVG,等函数。
SELECT column_name, function(column_name) FROM table_name WHERE column_name operator value GROUP BY column_name;
### 使用 WITH ROLLUP
WITH ROLLUP 可以实现在分组统计数据基础上再进行相同的统计（SUM,AVG,COUNT…）。

### MySQL 连接的使用
你可以在 SELECT, UPDATE 和 DELETE 语句中使用 Mysql 的 JOIN 来联合多表查询。
* INNER JOIN（内连接,或等值连接）：获取两个表中字段匹配关系的记录。
    * SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a INNER JOIN tcount_tbl b ON a.runoob_author = b.runoob_author;
    * SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a, tcount_tbl b WHERE a.runoob_author = b.runoob_author;
* LEFT JOIN（左连接）：获取左表所有记录，即使右表没有对应匹配的记录。
    * SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a LEFT JOIN tcount_tbl b ON a.runoob_author = b.runoob_author;
* RIGHT JOIN（右连接）： 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。
    * SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a RIGHT JOIN tcount_tbl b ON a.runoob_author = b.runoob_author;
    
### MySQL NULL 值处理
* IS NULL: 当列的值是 NULL,此运算符返回 true。
* IS NOT NULL: 当列的值不为 NULL, 运算符返回 true。
* <=>: 比较操作符（不同于 = 运算符），当比较的的两个值相等或者都为 NULL 时返回 true。

### MySQL 正则表达式
|模式|描述|
|---|---|
|^|	匹配输入字符串的开始位置。如果设置了 RegExp 对象的 Multiline 属性，^ 也匹配 '\n' 或 '\r' 之后的位置。|
|$|	匹配输入字符串的结束位置。如果设置了RegExp 对象的 Multiline 属性，$ 也匹配 '\n' 或 '\r' 之前的位置。|
|.|	匹配除 "\n" 之外的任何单个字符。要匹配包括 '\n' 在内的任何字符，请使用像 '[.\n]' 的模式。|
|[...]|	字符集合。匹配所包含的任意一个字符。例如， '[abc]' 可以匹配 "plain" 中的 'a'。|
|[^...]|	负值字符集合。匹配未包含的任意字符。例如， '[^abc]' 可以匹配 "plain" 中的'p'。|
|p1\|p2\|p3|	匹配 p1 或 p2 或 p3。例如，'z\|food' 能匹配 "z" 或 "food"。'(z\|f)ood' 则匹配 "zood" 或 "food"。|
| * |	匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。|
|+|	匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。|
|{n}|	n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。|
|{n,m}|	m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。|

### MySQL 事务
* 原子性：一个事务（transaction）中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被回滚（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。
* 一致性：在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设规则，这包含资料的精确度、串联性以及后续数据库可以自发性地完成预定的工作。
* 隔离性：数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。
* 持久性：事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。

        在 MySQL 命令行的默认设置下，事务都是自动提交的，即执行 SQL 语句后就会马上执行 COMMIT 操作。
        因此要显式地开启一个事务务须使用命令 EGIN 或 START TRANSACTION，或者执行命令 SET AUTOCOMMIT=0，用来禁止使用当前会话的自动提交。
### 事务控制语句：
* BEGIN 或 START TRANSACTION 显式地开启一个事务；

* COMMIT 也可以使用 COMMIT WORK，不过二者是等价的。COMMIT 会提交事务，并使已对数据库进行的所有修改成为永久性的；

* ROLLBACK 也可以使用 ROLLBACK WORK，不过二者是等价的。回滚会结束用户的事务，并撤销正在进行的所有未提交的修改；

* SAVEPOINT identifier，SAVEPOINT 允许在事务中创建一个保存点，一个事务中可以有多个 SAVEPOINT；

* RELEASE SAVEPOINT identifier 删除一个事务的保存点，当没有指定的保存点时，执行该语句会抛出一个异常；

* ROLLBACK TO identifier 把事务回滚到标记点；

* SET TRANSACTION 用来设置事务的隔离级别。InnoDB 存储引擎提供事务的隔离级别有READ UNCOMMITTED、READ COMMITTED、REPEATABLE READ 和 SERIALIZABLE。
### MySQL ALTER命令
当我们需要修改数据表名或者修改数据表字段时，就需要使用到MySQL ALTER命令。
#### 删除，添加或修改表字段
* ALTER TABLE testalter_tbl  DROP i;
* ALTER TABLE testalter_tbl ADD i INT;
#### 修改字段类型及名称
* ALTER TABLE testalter_tbl MODIFY c **CHAR(10)**;  //修改类型
* ALTER TABLE testalter_tbl CHANGE i **j BIGINT**;  //修改名称和类型
* ALTER TABLE testalter_tbl CHANGE j **j INT**;     //修改类型
#### ALTER TABLE 对 Null 值和默认值的影响
* ALTER TABLE testalter_tbl MODIFY j BIGINT NOT NULL DEFAULT 100;
如果你不设置默认值，MySQL会自动设置该字段默认为 NULL。
#### 修改字段默认值
* ALTER TABLE testalter_tbl ALTER i SET DEFAULT 1000; //设置字段默认值
ALTER TABLE testalter_tbl ALTER i DROP DEFAULT; //删除字段默认值
#### 修改表名
* ALTER TABLE testalter_tbl RENAME TO alter_tbl;
### MySQL 索引
#### 普通索引  //无任何限制
* 创建索引：CREATE INDEX indexName ON table_name (column_name(length)); //如果是CHAR，VARCHAR类型，length可以小于字段实际长度；如果是BLOB和TEXT类型，必须指定 length。
* 修改表结构(添加索引)：ALTER table tableName ADD INDEX indexName(columnName);
* 创建表的时候直接指定：CREATE TABLE mytable( ID INT NOT NULL, username VARCHAR(16) NOT NULL, INDEX [indexName] (username(length)) );  
* 删除索引的语法：DROP INDEX [indexName] ON mytable; 
#### 唯一索引  //索引列的值必须唯一，但允许有空值
* 创建索引:CREATE UNIQUE INDEX indexName ON mytable(username(length)) 
* 修改表结构(添加索引):ALTER table mytable ADD UNIQUE [indexName] (username(length))
* 创建表的时候直接指定:CREATE TABLE mytable( ID INT NOT NULL,  username VARCHAR(16) NOT NULL, UNIQUE [indexName] (username(length)) );  
### 使用ALTER 命令添加和删除索引
* ALTER TABLE tbl_name ADD PRIMARY KEY (column_list): 该语句添加一个主键，这意味着索引值必须是唯一的，且不能为NULL。
* ALTER TABLE tbl_name ADD UNIQUE index_name (column_list): 这条语句创建索引的值必须是唯一的（除了NULL外，NULL可能会出现多次）。
* ALTER TABLE tbl_name ADD INDEX index_name (column_list): 添加普通索引，索引值可出现多次。
* ALTER TABLE tbl_name ADD FULLTEXT index_name (column_list):该语句指定了索引为 FULLTEXT ，用于全文索引。
### 使用 ALTER 命令添加和删除主键
* ALTER TABLE testalter_tbl MODIFY i INT NOT NULL; //设置列不为空
* ALTER TABLE testalter_tbl ADD PRIMARY KEY (i); //设置列为主键索引
* ALTER TABLE testalter_tbl DROP PRIMARY KEY; //删除主键
### 显示索引信息
* SHOW INDEX FROM table_name \G(格式化输出信息）;
### MySQL 临时表
临时表只在当前连接可见，当关闭连接时，Mysql会自动删除表并释放所有空间。
* CREATE **TEMPORARY** TABLE SalesSummary (product_name VARCHAR(50) NOT NULL, total_sales DECIMAL(12,2) NOT NULL DEFAULT 0.00, avg_unit_price DECIMAL(7,2) NOT NULL DEFAULT 0.00, total_units_sold INT UNSIGNED NOT NULL DEFAULT 0);
### 删除MySQL 临时表
默认情况下，当你断开与数据库的连接后，临时表就会自动被销毁。当然你也可以在当前MySQL会话使用 DROP TABLE 命令来手动删除临时表。
* DROP TABLE SalesSummary
### MySQL 复制表
如果我们需要完全的复制MySQL的数据表，包括表的结构，索引，默认值等。 如果仅仅使用CREATE TABLE ... SELECT 命令，是无法实现的。只会复制表数据和表结构，不会有任何约束。
#### 第一种方法
* 步骤一：获取数据表的完整结构。
    * SHOW CREATE TABLE runoob_tbl \G;
* 步骤二：修改SQL语句的数据表名，并执行SQL语句。
* 步骤三：执行完第二步骤后，你将在数据库中创建新的克隆表 clone_tbl。 如果你想拷贝数据表的数据你可以使用 INSERT INTO...[AS] SELECT 语句来实现。
    * INSERT INTO clone_tbl (runoob_id,runoob_title,runoob_author, submission_date) SELECT runoob_id,runoob_title,runoob_author,submission_date FROM runoob_tbl;
* 执行以上步骤后，你将完整的复制表，包括表结构及表数据。    
#### 第二种方法
* 复制表结构
    * CREATE TABLE targetTable LIKE sourceTable;
    * create table 新表 select * from 旧表 where 1=2；//当 where 条件不成立时，只复制表结构，没有任务数据
* 复制表内容
    * INSERT INTO targetTable SELECT * FROM sourceTable;
### MySQL元数据    
|命令	描述|
|---|---|
|SELECT VERSION( )|	服务器版本信息|
|SELECT DATABASE( )|	当前数据库名 (或者返回空)|
|SELECT USER( )|	当前用户名|
|SHOW STATUS	|服务器状态|
|SHOW VARIABLES	|服务器配置变量|
### MySQL 序列使用
MySQL 序列是一组整数：1, 2, 3, ...，由于一张数据表只能有一个字段自增主键， 如果你想实现其他字段也实现自动增加，就可以使用MySQL序列来实现。
#### 使用 AUTO_INCREMENT
#### 获取AUTO_INCREMENT值
* 使用 SQL中的LAST_INSERT_ID( ) 函数
#### 重置序列
如果你删除了数据表中的多条记录，并希望对剩下数据的AUTO_INCREMENT列进行重新排列。
* ALTER TABLE insect DROP id;//删除id列
* ALTER TABLE insect ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT FIRST,ADD PRIMARY KEY (id);//添加id列
#### 设置序列的开始值
* create .....)auto_increment=100;
* ALTER TABLE t AUTO_INCREMENT = 100;
**********************
### MySQL 处理重复数据
#### 防止表中出现重复数据
* PRIMARY KEY（主键） 或者 UNIQUE（唯一） 索引来保证数据的唯一性。
* INSERT IGNORE INTO 与 INSERT INTO 的区别就是 INSERT IGNORE INTO 会忽略数据库中已经存在的数据，如果数据库没有数据，就插入新的数据，如果有数据的话就跳过这条数据。这样就可以保留数据库中已经存在数据，达到在间隙中插入数据的目的。
* REPLACE INTO 如果存在 primary 或 unique 相同的记录，则先删除掉。再插入新记录。
#### 统计重复数据
SELECT COUNT(\*) as repetitions, last_name, first_name
    -> FROM person_tbl
    -> GROUP BY last_name, first_name
    -> HAVING repetitions > 1;
#### 过滤重复数据
SELECT **DISTINCT** last_name, first_name
    -> FROM person_tbl;
#### 删除重复数据
**第一种方法**
* CREATE TABLE tmp SELECT last_name, first_name, sex FROM person_tbl  GROUP BY (last_name, first_name, sex);
* DROP TABLE person_tbl;
* ALTER TABLE tmp RENAME TO person_tbl;
**第二种方法**   
* ALTER IGNORE TABLE person_tbl ADD PRIMARY KEY (last_name, first_name);
### MySQL 及 SQL 注入
* 所谓SQL注入，就是通过把SQL命令插入到Web表单递交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令。
### MySQL 导出数据
#### 使用 SELECT ... INTO OUTFILE 语句导出数据
* SELECT * FROM runoob_tbl INTO OUTFILE '/tmp/runoob.txt';
你可以通过命令选项来设置数据输出的指定格式，以下实例为导出 CSV 格式:
SELECT * FROM passwd INTO OUTFILE '/tmp/runoob.txt'
    -> FIELDS TERMINATED BY ',' ENCLOSED BY '"'
    -> LINES TERMINATED BY '\r\n';
..........................................................................未完
### MySQL 导入数据		
1.mysql 命令导入
* mysql -u用户名  -p密码  < 要导入的数据库数据(runoob.sql)
2.source 命令导入
* mysql> create database abc;      # 创建数据库
* mysql> use abc;                  # 使用已创建的数据库 
* mysql> set names utf8;           # 设置编码
* mysql> source /home/abc/abc.sql  # 导入备份数据库
3.使用 LOAD DATA 导入数据
* LOAD DATA LOCAL INFILE 'dump.txt' INTO TABLE mytbl;
4.使用 mysqlimport 导入数据
* mysqlimport -u root -p --local mytbl dump.txt
* mysqlimport -u root -p --local --fields-terminated-by=":" --lines-terminated-by="\r\n"  mytbl dump.txt
* mysqlimport -u root -p --local --columns=b,c,a mytbl dump.txt
### mysqlimport的常用选项介绍
|选项	|功能|
|---|---|
|-d or --delete	|新数据导入数据表中之前删除数据数据表中的所有信息|
|-f or --force	|不管是否遇到错误，mysqlimport将强制继续插入数据|
|-i or --ignore	|mysqlimport跳过或者忽略那些有相同唯一 关键字的行， 导入文件中的数据将被忽略。|
|-l or -lock-tables	|数据被插入之前锁住表，这样就防止了， 你在更新数据库时，用户的查询和更新受到影响。|
|-r or -replace	|这个选项与－i选项的作用相反；此选项将替代 表中有相同唯一关键字的记录。|
|--fields-enclosed- by= char	|指定文本文件中数据的记录时以什么括起的， 很多情况下 数据以双引号括起。 默认的情况下数据是没有被字符括起的。|
|--fields-terminated- by=char	|指定各个数据的值之间的分隔符，在句号分隔的文件中， 分隔符是句号。您可以用此选项指定数据之间的分隔符。 默认的分隔符是跳格符（Tab）|
|--lines-terminated- by=str	|此选项指定文本文件中行与行之间数据的分隔字符串 或者字符。 默认的情况下mysqlimport以newline为行分隔符。 您可以选择用一个字符串来替代一个单个的字符： 一个新行或者一个回车。|
|-v| 显示版本（version）|
|-p |提示输入密码（password）|
### MySQL 函数
[MySQL 函数](https://www.runoob.com/mysql/mysql-functions.html)
### MySQL 运算符
[MySQL 运算符](https://www.runoob.com/mysql/mysql-operator.html)
lichao
