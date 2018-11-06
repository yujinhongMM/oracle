### 创建表空间
#### 创建表空间USERS
```sql
CREATE TABLESPACE users DATAFILE 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users.dbf' 
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED, 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users.dbf'  
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED 
EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
```
#### 创建表空间USERS02
```sql
CREATE TABLESPACE users02 DATAFILE 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users02_1.dbf' 
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED, 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users02_2.dbf'  
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED 
EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
```
#### 创建表空间USERS03
```sql
CREATE TABLESPACE users03 DATAFILE 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users03_1.dbf' 
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED, 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users03_2.dbf'  
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED 
EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
```

