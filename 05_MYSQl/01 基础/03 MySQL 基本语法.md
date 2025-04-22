# 1.查看所有的数据库
```
show databases;
```

> * “information_schema”是 MySQL 系统自带的数据库，主要保存 MySQL 数据库服务器的系统信息，比如数据库的名称、数据表的名称、字段名称、存取权限、数据文件 所在的文件夹和系统使用的文件夹，等等
> * “performance_schema”是 MySQL 系统自带的数据库，可以用来监控 MySQL 的各类性能指标。
> * “sys”数据库是 MySQL 系统自带的数据库，主要作用是以一种更容易被理解的方式展示 MySQL 数据库服务器的各类性能指标，帮助系统管理员和开发人员监控 MySQL 的技术性能。
> * “mysql”数据库保存了 MySQL 数据库服务器运行时需要的系统信息，比如数据文件夹、当前使用的字符集、约束检查信息，等等

为什么 Workbench 里面我们只能看到“demo”和“sys”这 2 个数据库呢？

> 这是因为，Workbench 是图形化的管理工具，主要面向开发人 员，“demo”和“sys”这 2 个数据库已经够用了。如果有特殊需求，比如，需要监控 MySQL 数据库各项性能指标、直接操作 MySQL 数据库系统文件等，可以由 DBA 通过 SQL 语句，查看其它的系统数据库。

# 2.创建自己的数据库

```
creat database 数据库名;
创建的数据库名不能与已经存在的数据库名重复
```

# 3. 使用自己的数据库
```
use 数据库命;
```

**说明**：如果没有使用use语句，后面针对数据库的操作也没有加“数据名”的限定，那么会报“ERROR 1046

(3D000): No database selected”（没有选择数据库）

使用完use语句之后，如果接下来的SQL都是针对一个数据库操作的，那就不用重复use了，如果要针对另一个数据库操作，那么要重新use。

# 4. 查看某个库的所有表格
```
show tables;
要求前面有使用过use
```

# 5. 创建新的表格
```
creat table 表名称(
	字段名 数据类型,
	字段名 数据类型
	);
```

说明：如果是最后一个字段，后面就用加逗号，因为逗号的作用是分割每个字段。

# 6. 查看一个表的数据
```
select from 数据库名称;
```

# 7. 添加一条记录

```
insert into 表名称 values (值列表)

例如：
insert into student valuse(100,'李四');
```


# 8. 查看表的创建信息
```
show create table 表名称;
```

# 9. 查看数据库的创建信息

```
show create database 数据库名;
```

# 10. 删除表格

```
drop table 表格名;
```

# 11. 删除数据库
```
drop database 数据库名称;
```

# 12. 查看编码命令
```
show variables like "character_%"
show vatiables like "collation_%"
```


