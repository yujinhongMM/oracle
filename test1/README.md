# oracle
**查询1** 

<table><tr><td bgcolor=#7FFFD4>SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资" 

from hr.departments d，hr.employees e 

where d.department_id = e.department_id 

and d.department_name in ('IT'，'Sales') 

GROUP BY department_name;</td></tr></table>

![1](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192608.png)
![2](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192634.png)
![3](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192641.png)
![4](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192648.png)
![5](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192658.png)
![6](https://github.com/yujinhongMM/oracle/blob/master/test1/QQ%E5%9B%BE%E7%89%8720181016192707.png)
