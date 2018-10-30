# oracle实验二
## 一、实验步骤
### 第1步：连接到服务器
 
```sql
$ ssh oracle@202.115.82.8
oracle@202.115.82.8's password:
[oracle@deep02 ~]$
```
![1](https://github.com/yujinhongMM/oracle/blob/master/test2/1.png) 
### 第2步：以system登录到pdborcl，创建角色 *con_res_view0* 和用户 *new_user0* ，并授权和分配空间：
 
```sql
$ sqlplus system/123@pdborcl
SQL> CREATE ROLE con_res_view0;
Role created.
SQL> GRANT connect,resource,CREATE VIEW TO con_res_view0;
Grant succeeded.
SQL> CREATE USER new_user0 IDENTIFIED BY 123 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
User created.
SQL> ALTER USER new_user0 QUOTA 50M ON users;
User altered.
SQL> GRANT con_res_view0 TO new_user0;
Grant succeeded.
SQL> exit
```
![2](https://github.com/yujinhongMM/oracle/blob/master/test2/2.png) 
![3](https://github.com/yujinhongMM/oracle/blob/master/test2/3.png) 
### 第3步：新用户new_user0连接到pdborcl，创建表mytable和视图myview，插入数据，最后将myview的SELECT对象权限授予hr用户。
```sql
sqlplus new_user0/123@pdborcl
SQL> show user;
USER is "NEW_USER0"
SQL> CREATE TABLE mytable (id number,name varchar(50));
Table created.
SQL> INSERT INTO mytable(id,name)VALUES(1,'zhang');
1 row created.
SQL> INSERT INTO mytable(id,name)VALUES (2,'wang');
1 row created.
SQL> CREATE VIEW myview AS SELECT name FROM mytable;
View created.
SQL> SELECT * FROM myview;
NAME
--------------------------------------------------
zhang
wang
SQL> GRANT SELECT ON myview TO hr;
Grant succeeded.
SQL>exit
```
![4](https://github.com/yujinhongMM/oracle/blob/master/test2/4.png) 
### 第4步：用户hr连接到pdborcl，查询new_user0授予它的视图myview
```sql
$ sqlplus hr/123@pdborcl
SQL> SELECT * FROM new_user.myview;
NAME
--------------------------------------------------
zhang
wang
SQL> exit
```
![5](https://github.com/yujinhongMM/oracle/blob/master/test2/5.png)
## 二、查看数据库的使用情况
以下样例查看表空间的数据库文件，以及每个文件的磁盘占用情况。
```sql
sqlplus system/123@pdborcl
SQL>SELECT tablespace_name,FILE_NAME,BYTES/1024/1024 MB,MAXBYTES/1024/1024 MAX_MB,autoextensible FROM dba_data_files  WHERE  tablespace_name='USERS';

SQL>SELECT a.tablespace_name "表空间名",Total/1024/1024 "大小MB",
 free/1024/1024 "剩余MB",( total - free )/1024/1024 "使用MB",
 Round(( total - free )/ total,4)* 100 "使用率%"
 from (SELECT tablespace_name,Sum(bytes)free
        FROM   dba_free_space group  BY tablespace_name)a,
       (SELECT tablespace_name,Sum(bytes)total FROM dba_data_files
        group  BY tablespace_name)b
 where  a.tablespace_name = b.tablespace_name;
```
![6](https://github.com/yujinhongMM/oracle/blob/master/test2/6.png)
![7](https://github.com/yujinhongMM/oracle/blob/master/test2/7.png) 

autoextensible是显示表空间中的数据文件是否自动增加。 

MAX_MB是指数据文件的最大容量。
## 三、实验参考
Oracle地址：202.115.82.8 用户名：system,hr,new_user ， 密码123， 数据库名称：pdborcl，端口号：1521 
SQL-DEVELOPER修改用户的操作界面：

![8](https://github.com/yujinhongMM/oracle/blob/master/test2/8.png) 
![9](https://github.com/yujinhongMM/oracle/blob/master/test2/9.png)  
![10](https://github.com/yujinhongMM/oracle/blob/master/test2/10.png) 

sqldeveloper授权对象的操作界面：

![11](https://github.com/yujinhongMM/oracle/blob/master/test2/11.png)  
![12](https://github.com/yujinhongMM/oracle/blob/master/test2/12.png)


