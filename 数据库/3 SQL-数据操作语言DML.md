1. 查询表中的所有数据：

   ```mysql
   select * from 表名;
   ```

   > 可以在“表名”后面加上"\G"，换一种输出方式

2. 插入操作：

   ```mysql
   insert into 表名(列名1,列名2,...) values(列值1,列值2,...),(...),(...)...;
   ```

   

3. 更新操作：

   ```mysql
   update 表名 set 字段1=值1, 字段2=值2 ... where 字段=值;
   ```

   **修改数据库密码：**

   **方法一：**

   * MySQL用户信息存在`mysql`数据库中的`user`表中

   * `password()`是将密码加密的函数
   * `flush privilege;`刷新系统权限，只有用了这个操作，才能将密码修改

   ```mysql
   update mysql.user set authentication_string=password('新密码') where user='root' and Host='localhost';
   flush privilege;
   ```

   **方法二：**

   在`cmd`中敲：

   `mysqladmin -u root -p password 新密码`

   

4. 删除操作：

   ```mysql
   -- 删除某一/某些数据元素：
   delete from 表名 where 字段=值;
   
   -- 删除所有数据：
   delete from 表名;
   
   -- 直接将表删除，然后再创建一个同样的新表，删除的数据不能找回，执行速度比delete快：
   truncate table 表名;
   ```

   

   

