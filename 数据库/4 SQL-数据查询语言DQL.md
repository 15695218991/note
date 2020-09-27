1. 查询所有列：

   ```mysql
   select * from 表名;
   ```

   

2. 查询指定的列：

   ```mysql
   select 列名1,列名2,... from 表名;
   ```

   

3. 条件查询：

   **用`where`语句：**

   * `=`等于
   * `!=`不等于
   * `<>`不等于
   * `BETWEEN...AND...` 值在什么范围
   * `IN(set)`固定的范围值
   * `IS NULL`为空，`IS NOT NULL`不为空
   * `AND`与，`OR`或，`NOT`非

   ```mysql
   -- 查询id为1001,1002,1003的记录
   -- 方法1：
   select * from students where id=1001 or id=1002 or id=1003;
   -- 方法2：
   select * from students where id in(1001,1002,1003);
   
   -- 查询name为null的记录
   select * from students where name is null;
   
   -- 查询age在18到20之间的记录
   -- 方法1：
   select * from students where age>=18 and age<=20;
   -- 方法2：
   select * from students where age between 18 and 20;
   ```

   

4. 模糊查询

   **用`like`语句，通配符：**

   * `_`任意一个字符
   * `%`任意0个或多个字符

   ```mysql
   -- 查询姓名由5个字符构成的记录
   select * from students where name like '_____';   -- 其中有5个'_'
   
   -- 查询姓名由5个字符构成，且第5个字符为"s"的记录
   select * from students where name like '____s';   -- 其中有4个'_'
   
   -- 查询姓名以"m"开头的记录
   select * from students where name like 'm%';
   
   -- 查询姓名第2个字符为"u"的记录
   select * from students where name like '_u%';
   
   -- 查询姓名中包含"s"字符的记录
   select * from students where name like '%s%';
   ```

   

5. 字段控制查询

   ```mysql
   -- 去重查询(distinct)
   select distinct 字段名 from 表名;
   
   -- 查询所有字段，并计算字段age和name之和，将计算结果添加到查询结果中
   select *,age+score from students;
   
   -- 上一例中将age+score为null的改为0
   -- ifnull()函数：若参数1的值为null，就将其改为参数2
   -- as语句：将新添加的列改名为total
   select *,ifnull(age,0)+ifnull(score,0) as total from students;
   ```

   

6. 排序

   ```mysql
   -- 以字段salary升序排序(默认的方式)
   select * from students order by salary asc;
   
   -- 以字段salary降序排序
   select * from students order by salary desc;
   
   -- 如果salary相同，就以字段id降序排序
   select * from students order by salary desc, id desc;
   ```

   

7. 聚合函数

   * `count()`：可以统计字段不为null的数据条数
   * `sum()`：求和
   * `avg()`：求均值
   * `max()`：求最大值
   * `min()`：求最小值

   ```mysql
   -- 统计总共有多少条数据
   select count(*) from students;
   -- 统计id字段不为null的数据条数
   select count(id) from students;
   -- 统计salary大于2500的数据条数
   select count(*) from students where salary > 2500;
   -- 统计salary与performance之和大于5000的数据条数
   select count(*) from students where ifnull(salary,0) + ifnull(performance,0) > 5000;
   
   -- 求所有数据中salary之和
   select sum(salary) from students;
   
   -- 求所有数据中salary的均值
   select avg(salary) from students;
   ```

   

8. 分组查询

   将字段值相同的划分为一组

   * 当`group by`单独使用时，只显示出每组的第一条记录

   ```mysql
   -- 通过gender分组，并查询每组中的name
   -- group by 后面出现的字段，一般在前面也会出现
   select gender,group_concat(name) from students group by gender;
   
   -- 查询每个分组中的salary总和
   -- 若有group by分组，聚合函数统计的就是本组内的数据
   select gender,sum(salary) from students group by gender;
   
   -- 查询每个部门的department名称以及每个department中salary大于1500的人数
   select department,group_concat(salary),count(*) from employee where salary > 1500 group by department;
   ```

   

9. group by + having

   **having 与 where的区别：**

   * `having`是在分组后对数据进行过滤，`where`是在分组前对数据进行过滤
   * `having`后面可以使用分组函数（统计函数），`where`后面不可以使用分组函数

   ```mysql
   -- 查询工资综合大于9000的部门名称
   select department,group_concat(salary),sum(salary) from employee 
   group by department 
   having sum(salary) >= 9000;
   
   -- 查询工资大于2000的，工资总和大于6000的部门名称以及工资和
   select department,group_concat(salary),sum(salary) from employee 
   where salary > 2000 
   group by department 
   having sum(salary) > 9000
   order by sum(salary) desc;
   ```

   

10. 书写顺序与执行顺序

    **书写顺序：**

    `select --> from --> where --> group by --> having --> order by --> limit `

    **执行顺序：**

    `from --> where --> group by --> having --> select --> order by --> limit`

    

11. limit

    ```mysql
    -- 选employee表中的前三条数据
    select * from employee limit 0,3;   -- 从第1条数据开始，选3条
    -- 选employee表中的第7-10条数据
    select * from employee limit 6,4;   -- 从第7条数据开始，选4条
    ```

    