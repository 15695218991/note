> 一般关键字大写，自己定义的东西小写

1. 创建数据库：

   ```mysql
   create database 数据库名 character set utf8;
   ```

2. 创建表：

   > (约束)指的是长度

   ```mysql
   create table 表名{
   	列名1 列的类型 (约束),
   	列名2 列的类型 (约束),
   	...,
   	列名N 列的类型 (约束)
   };
   ```

3. 创建学生表：

4. 查看表的字段信息：

   ```mysql
   desc 表名;
   ```

5. 添加一列（add）：

   ```mysql
   alter table 表名 add 列名 数据类型;
   ```

6. 修改一个表的字段类型（modify）：

   ```mysql
   alter table 表名 modify 字段名 数据类型;
   ```

7. 删除一列（drop）：

   ```mysql
   alter table 表名 drop 字段名;
   ```

8. 修改表的字符集：

   ```mysql
   alter table 表名 character set gbk;
   ```

9. 修改表名：

   ```mysql
   rename table 原始表名 to 修改的表名;
   ```

10. 修改表中的列名：

    ```mysql
    alter table 表名 change 原字段名 修改的字段名 数据类型;
    ```

11. 查看表的创建细节：

    ```mysql
    show create table 表名;
    ```

12. 删除表：

    ```mysql
    drop table 表名;
    ```