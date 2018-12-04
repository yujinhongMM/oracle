# oracle
# 1.所要用到的查询语句
## 1.1查询1

```
SELECT d.department_name，count(e.job_id)as "部门总人数"， 
avg(e.salary)as "平均工资"  
from hr.departments d，hr.employees e  
where d.department_id = e.department_id  
and d.department_name in ('IT'，'Sales')  
GROUP BY department_name; 
```
## 1.2查询2 
 
```
SELECT d.department_name，count(e.job_id)as "部门总人数"， 
avg(e.salary)as "平均工资"  
FROM hr.departments d，hr.employees e  
WHERE d.department_id = e.department_id  
GROUP BY department_name  
HAVING d.department_name in ('IT'，'Sales');  
``` 

# 2.sqlplus 
## 2.1连接
![1](https://github.com/yujinhongMM/oracle/blob/master/test1/1.png) 
## 2.2查询1
![1](https://github.com/yujinhongMM/oracle/blob/master/test1/2.png) 
![1](https://github.com/yujinhongMM/oracle/blob/master/test1/3.png)
## 2.3查询2
![1](https://github.com/yujinhongMM/oracle/blob/master/test1/4.png) 
![1](https://github.com/yujinhongMM/oracle/blob/master/test1/5.png)

# 3.sql developer 
## 3.1连接
![1](https://github.com/yujinhongMM/oracle/blob/master/test1/6.png) 
## 3.2查询1
![1](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192608.png) 
![2](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192634.png)
![3](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192641.png) 
## 3.3查询2
![4](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192648.png)
![5](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192658.png)
![6](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192707.png)

# 4.你认为那个查询语句最优？  
 <font color=#0099ff size=7 face="黑体"> 我认为查询语句1更优。 </font>
