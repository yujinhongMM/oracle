# oracle
oracle实验
创建表空间
CREATE TABLESPACE users02 DATAFILE 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users02_1.dbf' 
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED, 
'E:/oracle/app/oracle/oradata/orcl/pdborcl/pdbtest_users02_2.dbf'  
  SIZE 100M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED 
EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
