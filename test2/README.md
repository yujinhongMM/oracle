# oracle实验二
## 第1步：连接到服务器
 
```sql
$ ssh oracle@202.115.82.8
oracle@202.115.82.8's password:
[oracle@deep02 ~]$
```
![1](https://github.com/yujinhongMM/oracle/blob/master/test2/1.png) 
## 第2步：以system登录到pdborcl，创建角色con_res_view0和用户new_user0，并授权和分配空间：
 
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
## 第3步：新用户new_user0连接到pdborcl，创建表mytable和视图myview，插入数据，最后将myview的SELECT对象权限授予hr用户。
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
![2](https://github.com/yujinhongMM/oracle/blob/master/test2/4.png) 





