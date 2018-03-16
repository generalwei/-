登录MySQL
mysql -u root -p 
-------------------------------------------------------------------------------
修改密码
格式：mysqladmin -u用户名 -p旧密码 password 新密码
-------------------------------------------------------------------------------
添加新用户
允许本地 IP 访问 localhost, 127.0.0.1
create user 'test'@'localhost' identified by '123456';  

允许外网 IP 访问
create user 'test'@'%' identified by '123456'; 

刷新授权
flush privileges;  
-------------------------------------------------------------------------------
查询所有数据库
show databases;

显示use的数据库名
SELECT DATABASE();

为用户创建数据库
create database 库名 DEFAULT CHARSET utf8 COLLATE utf8_general_ci;

删除数据库
DROP DATABASE 库名;
-------------------------------------------------------------------------------
为新用户分配权限
授予用户通过外网IP对于该数据库的全部权限
grant all privileges on `testdb`.* to 'test'@'%' identified by '123456'; 

授予用户在本地服务器对该数据库的全部权限
grant all privileges on `testdb`.* to 'test'@'localhost' identified by '123456';  

刷新权限
flush privileges; 

退出 root 重新登录
exit

用新帐号 test 重新登录，由于使用的是 % 任意IP连接，所以需要指定外部访问IP
mysql -u test -h 115.28.203.224 -p  

在Ubuntu服务器下，MySQL默认是只允许本地登录，因此需要修改配置文件将地址绑定给注释掉：
# Instead of skip-networking the default is now to listen only on  
# localhost which is more compatible and is not less secure.  
#bind-address       = 127.0.0.1     #注释掉这一行就可以远程登录了  
-------------------------------------------------------------------------------
MySQL基本操作
一、清除mysql表中数据
delete from 表名;
truncate table 表名;
效率上truncate比delete快，但truncate删除后不记录mysql日志，不可以恢复数据。
delete的效果有点像将mysql表中所有记录一条一条删除到删完，
而truncate相当于保留mysql表的结构，重新创建了这个表，所有的状态都相当于新表

二、删除表中的某些数据
delete from命令格式：delete from 表名 where 表达式

三、选择数据库
use 数据库名;

四、查询所有数据表
show tables;

五、数据库某表的备份,在命令行中输入
mysqldump -u root -p database_name table_name > bak_file_name;

六、导出数据
select_statment into outfile”dest_file”;

七、导入数据
load data infile”file_name” into table table_name;

八、删除字段
alter table form1 drop column 列名;

九、导入.sql文件命令
mysql> USE 数据库名;
mysql> SOURCE d:/mysql.sql;
也可以在DOS环境下键入以下命令进行导入：
mysql -uroot -proot databasename < databasename.sql

