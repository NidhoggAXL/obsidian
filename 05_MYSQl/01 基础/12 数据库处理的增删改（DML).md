[[第11章_数据处理之增删改.pdf]]
# 一、插入 (INSERT INTO) 数据

## 1.1 方式1：VALUES 的方式添加
使用这种语法一次只能向表中插入**一条**数据。

**情况1：为表的所有字段按默认顺序插入数据**
语法：
```mysql
INSERT INTO 表名 VALUES (value1,value2,....);
```

* 值列表中需要为表的每一个字段指定值，并且值的顺序必须和数据表中字段定义时的顺序相同。
* 要知道表中每个字段的类型，然后按照类型来进行编写

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1712817982000g1rugn.png)


**情况2（推荐）：为表的指定字段插入数据**
```mysql
INSERT INTO 表名(column1 [, column2, …, columnn]) VALUES (value1 [,value2, …, valuen]);
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1712818146000ag92it.png)

> 没有进行赋值，则默认为 null

**情况3（推荐）：添加多条记录**
NSERT语句可以同时向数据表中插入多条记录，插入时指定多个值列表，每个值列表之间用逗号分隔 开，基本语法格式如下：
```mysql
INSERT INTO table_name 
VALUES 
(value1 [,value2, …, valuen]), 
(value1 [,value2, …, valuen]), 
…… 
(value1 [,value2, …, valuen]);
```

或者
```mysql
INSERT INTO table_name(column1 [, column2, …, columnn]) 
VALUES (value1 [,value2, …, valuen]), 
(value1 [,value2, …, valuen]), 
…… 
(value1 [,value2, …, valuen]);
```

使用INSERT同时插入多条记录时，MySQL会返回一些在执行单行插入时没有的额外信息，这些信息的含 义如下： 
* Records：表明插入的记录条数。
* Duplicates：表明插入时被忽略的记录，原因可能是这 些记录包含了重复的主键值。
* Warnings：表明有问题的数据值，例如发生数据类型转换。

> 一个同时插入多行记录的INSERT语句等同于多个单行插入的INSERT语句，但是多行的INSERT语句 在处理过程中 效率更高 。因为MySQL执行单条INSERT语句插入多行数据比使用多条INSERT语句 快，所以在插入多条记录时最好选择使用单条INSERT语句的方式插入。

**小结**
* VALUES 也可以写成 VALUE ，但是VALUES是标准写法。 
* 字符和日期型数据应包含在单引号中。
## 1.2 方式2：将查询结果插入到表中
INSERT还可以将SELECT语句查询的结果插入到表中，此时不需要把每一条记录的值一个一个输入，只需 要使用一条INSERT语句和一条SELECT语句组成的组合语句即可快速地从一个或多个表中向一个表中插入 多行。 

基本语法格式如下：
```mysql
INSERT INTO 目标表名 
(tar_column1 [, tar_column2, …, tar_columnn]) 
SELECT (src_column1 [, src_column2, …, src_columnn]) 
FROM 源表名 
[WHERE condition]
```

* 在 INSERT 语句中加入子查询。 
* 不必书写 VALUES 子句。 
* 子查询中的值列表应与 INSERT 子句中的列名对应。

举例：
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1712819316000ddj9zt.png)

>[!tip] 说明：
>在一个表中添加查询时，要注意字段的类型大小的匹配，**字段可以大，但是不可以小**
# 二、更新（UPDATE) 数据
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17128198530005b98iq.png)

使用 UPDATE 语句更新数据。语法如下：
```mysql
UPDATE table_name 
SET column1=value1, column2=value2, … , column=valuen 
[WHERE condition]
```

* 可以一次更新多条数据,进行 WHERE 条件的设定，如果没有设定，那么就是默认全部修改。 
* 如果需要回滚数据，需要保证在DML前，进行设置：SET AUTOCOMMIT = FALSE;

使用 WHERE 子句指定需要更新的数据：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1712820313000rn06od.png)

如果省略 WHERE 子句，则表中的所有数据都将被更新：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1712820386000ztbar9.png)

**更新中的数据完整性错误**
```mysql
UPDATE employees SET   department_id = 55 WHERE department_id = 110;
```
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1712820505000utfu57.png)

> 不存在 55 号部门


# 三、删除（DELETE) 数据
使用 DELETE 语句从表中删除数据
```MYSQL
DELETE FROM table_name 
[WHERE <condition>];
```

* 使用 WHERE 子句删除指定的记录。
* 如果省略 WHERE 子句，则表中的全部数据将被删除
* **删除中的数据完整性错误**-外键约束的结果






# 四、MySQL8 新特性：计算列
什么叫计算列呢？简单来说就是某一列的值是通过别的列计算得来的。例如，a列值为1、b列值为2，c列 不需要手动插入，定义a+b的结果为c的值，那么c就是计算列，是通过别的列计算得来的。

在MySQL 8.0中，CREATE TABLE 和 ALTER TABLE 中都支持增加计算列。下面以CREATE TABLE为例进行讲 解。 

> GENERATED - generated - 产生的
> ALWAYS - always - 总是
>  VIRTUAL- virtual - 虚拟

举例：定义数据表tb1，然后定义字段id、字段a、字段b和字段c，其中字段c为计算列，用于计算a+b的 值。 首先创建测试表tb1，语句如下：
```mysql
CREATE TABLE tb1(
id INT, 
a INT, 
b INT, 
c INT GENERATED ALWAYS AS (a + b) VIRTUAL 
);
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1712821595000hglz1v.png)

修改字段的数据：**c 也会跟着改变**
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1712821674000qdzhe4.png)




