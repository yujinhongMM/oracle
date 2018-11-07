# oracle实验三
#### 自己电脑上安装的oracle用户*C##new_user0*，服务器上的用户为*new_user0*,实验步骤来自自己电脑上安装的oracle
## 以system登录
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
![1](https://github.com/yujinhongMM/oracle/blob/master/test3/1.png) 
#### 创建表空间USERS03
```sql
CREATE TABLESPACE users03 DATAFILE 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users03_1.dbf' 
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED, 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users03_2.dbf'  
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED 
EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
```
![1](https://github.com/yujinhongMM/oracle/blob/master/test3/2.png) 
#### 给自己的账号分配USERS,USERS02,USERS03三个分区的使用权限
```sql
ALTER USER C##new_user0 QUOTA 50M ON USERS;
ALTER USER C##new_user0 QUOTA 50M ON USERS02;
ALTER USER C##new_user0 QUOTA 50M ON USERS03;
```
![1](https://github.com/yujinhongMM/oracle/blob/master/test3/3.png) 

## 以C##new_user0登录
### 在表空间中创建两张表：订单表(orders)与订单详表(order_details)
#### 创建订单表(orders)
```sql
  CREATE TABLE "ORDERS" 
   (	"ORDER_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"CUSTOMER_NAME" VARCHAR2(40 BYTE) NOT NULL ENABLE, 
	"CUSTOMER_TEL" VARCHAR2(40 BYTE) NOT NULL ENABLE, 
	"ORDER_DATE" DATE NOT NULL ENABLE, 
	"EMPLOYEE_ID" NUMBER(6,0) NOT NULL ENABLE, 
	"DISCOUNT" NUMBER(8,2) DEFAULT 0, 
	"TRADE_RECEIVABLE" NUMBER(8,2) DEFAULT 0, 
	 CONSTRAINT "ORDERS_PK" PRIMARY KEY ("ORDER_ID")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  TABLESPACE "USERS"  ENABLE
   ) PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 
 NOCOMPRESS 
  STORAGE(
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "USERS" 
  PARTITION BY RANGE ("ORDER_DATE") 
 (PARTITION "PARTITION_BEFORE_2016"  VALUES LESS THAN (TO_DATE(' 2016-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))   NO INMEMORY SEGMENT CREATION DEFERRED 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 
 NOCOMPRESS NOLOGGING 
  STORAGE( INITIAL 8388608 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "USERS" , 
 PARTITION "PARTITION_BEFORE_2017"  VALUES LESS THAN (TO_DATE(' 2017-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN')) SEGMENT CREATION DEFERRED 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 
 NOCOMPRESS NOLOGGING 
  STORAGE(
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "USERS02"，
 
 PARTITION "PARTITION_BEFORE_2018"  VALUES LESS THAN (TO_DATE(' 2018-01-01 00:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN')) SEGMENT CREATION DEFERRED 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 
 NOCOMPRESS NOLOGGING 
  STORAGE(
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "USERS03"  ) ;
```
![1](https://github.com/yujinhongMM/oracle/blob/master/test3/4.png) 
#### 创建订单详表(order_details)
```sql
CREATE TABLE order_details 
(
id NUMBER(10, 0) NOT NULL 
, order_id NUMBER(10, 0) NOT NULL
, product_id VARCHAR2(40 BYTE) NOT NULL 
, product_num NUMBER(8, 2) NOT NULL 
, product_price NUMBER(8, 2) NOT NULL 
, CONSTRAINT order_details_fk1 FOREIGN KEY  (order_id)
REFERENCES orders  (  order_id   )
ENABLE 
) 
TABLESPACE USERS 
PCTFREE 10 INITRANS 1 
STORAGE (   BUFFER_POOL DEFAULT ) 
NOCOMPRESS NOPARALLEL
PARTITION BY REFERENCE (order_details_fk1)
(
PARTITION PARTITION_BEFORE_2016 
NOLOGGING 
TABLESPACE USERS
PCTFREE 10 INITRANS 1 
STORAGE 
( 
 INITIAL 8388608 
 NEXT 1048576 
 MINEXTENTS 1 
 MAXEXTENTS UNLIMITED 
 BUFFER_POOL DEFAULT 
) 
NOCOMPRESS NO INMEMORY, 
PARTITION PARTITION_BEFORE_2017 
NOLOGGING 
TABLESPACE USERS02
PCTFREE 10 INITRANS 1 
STORAGE 
( 
 INITIAL 8388608 
 NEXT 1048576 
 MINEXTENTS 1 
 MAXEXTENTS UNLIMITED 
 BUFFER_POOL DEFAULT 
) 
NOCOMPRESS NO INMEMORY, 
PARTITION PARTITION_BEFORE_2018 
NOLOGGING 
TABLESPACE USERS03
);
```
![1](https://github.com/yujinhongMM/oracle/blob/master/test3/5.png) 
#### 插入数据
```sql
declare
  maxnumber constant int:=10000;
  i int :=1;
  
begin

  for i in 1..maxnumber loop
  
    insert into orders(order_id, customer_name, customer_tel, order_date, employee_id, discount, trade_receivable)
    values(i, '1', '1', '1', '1', '1', '1');
    
    insert into order_details (id, order_id, product_id, product_num, product_price)
    values(i, '1', '1', '1', '1');
    
  end loop;
  commit;
  
end; 
```
## 以system登录
### 查看数据库的使用情况
#### 查看表空间的数据库文件，以及每个文件的磁盘占用情况
```sql
SELECT tablespace_name,FILE_NAME,BYTES/1024/1024 MB,MAXBYTES/1024/1024 MAX_MB,autoextensible FROM dba_data_files  WHERE  tablespace_name='USERS';
```
![1](https://github.com/yujinhongMM/oracle/blob/master/test3/6(1).png) 
```sql
SELECT a.tablespace_name "表空间名",Total/1024/1024 "大小MB",
 free/1024/1024 "剩余MB",( total - free )/1024/1024 "使用MB",
 Round(( total - free )/ total,4)* 100 "使用率%"
 from (SELECT tablespace_name,Sum(bytes)free
        FROM   dba_free_space group  BY tablespace_name)a,
       (SELECT tablespace_name,Sum(bytes)total FROM dba_data_files
        group  BY tablespace_name)b
 where  a.tablespace_name = b.tablespace_name;
 ```
 ![1](https://github.com/yujinhongMM/oracle/blob/master/test3/7.png) 




