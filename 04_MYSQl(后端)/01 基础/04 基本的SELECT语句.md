# 一、SQL 的概述
## 1.1 SQL  分类

> [!tip] DDL: (Data Definition Languages) 数据定义语言
> 这些语句定义了不同的数据库、表、视图、索引等数据库对象，还可以用来创建、删除、修改数据库和数据表的结构。
> * CREATE - create 创建
> * ALTET - altet 修改
> * DROP - drop 删除
> * ERNAME - rename 重命名
> * TRUNCATE - truncate 清空

> [!tip] DML (Data Manipulation Language) 数据操作语言
> 用于添加、删除、更新和查询数据库记录，并检查数据完整性
> * **SELECT 是SQL语言的基础，最为重要**
> * INSERT - insert 插入 (添加一条记录)
> * DELETE - delete 删除 (删除一条记录)
> * UPDATE - update 更新 (更新一条记录)
> * SELECT - select 选择 (查找)


> [!tip] DCL (Data Control Language) 数据控制语言
> 用于定义数据库、表、字段、用户的访问权限和安全级别。
> * COMMIT - commit 承诺 (提交更改记录)
> * ROLLBACK - rollback 回复 (撤销)
> * SAVEPOINT - sabepoint  save-保存 point-点  (保存点)
> * CRANT - crant (赋予相关的权限)
> * REVOKE - revoke  撤销 (回收相关的权限)

> [!tip] 
> 因为查询语句使用的非常的频繁，所以很多人把查询语句单拎出来一类:DQL(数据查询语言)还有单独将 COMMIT、ROLLBACK 取出来称为TCL(Transaction Control Language，事务控制语言)

# 二、SQL 语句的规则和规范

## 2.1 推荐采用统一的书写规范

> [!abstract]
> * 数据库名、表名、表别名、字段名、字段别名等都小写
> * SQL关键字、函数名、绑定变量等都大写

## 2.2 注释

> [!abstract]
> 单行注释：#注释文字 ( MySQL特有的方式 )
> 单行注释：-- 注释文字 (--后面必须包含一个空格) 大多数数据库都通用
> 多行注释：/* 注释文字 */

# 三、基本的SELLECT 语句
## 3.0 SELECT……

```sql
SELECT 1;#没有任何语句
SELECT 2*3；
```

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171187392700071zsx4.png)

## 3.1 SELECT…FROM…

```sql
SELECT 标识选择那些列
FROM   标识从那个表中选择
```

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711874187000twdjol.png)

* 伪表

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711874275000xyr1ur.png)

* 查询所有的字段 (或列)

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711874371000ifdl7r.png)

## 3.2 别名(alias)

可以使用下面的方法进行别名的设置：
* `SELSCT 原名 别名`
* `SELSCT 原名 AS 别名`
* `SELSCT 原名 AS "别名"`
	* 当别名里面有空格时就要使用""号了

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711883064000j4roiv.png)

## 3.3 去除重复行

默认情况下，查询会放回全部行，包括重复行。

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17118836680003kc2ye.png)

如果不想查询到重复的数据，就要使用关键字 distinct (不同的：明显的) ：

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711883771000ax0z7d.png)

> [!tip] distinct使用注意事项
> 查询多个数据的时候不能把 distinct 放在字段的后面：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17118839300009fp4ex.png)

# 3.4 空值的参与和运算
1. 空值：null
2. ** null 不等同于 0，'','null'**
3. 空值参与运算：结果一定也为空。![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711884624000ql455m.png)
4. 如果要解决这个问题，那么使用关键字 ifnull ：
	1. ifnull (字段名，0) 如果这个字段为 null 的话就是0，不为 null 则就是字段本来的值。
	2. ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711885081000ute61g.png)


# 3.5 着重号(反引号)
必须保证你的字段没有和保留字、数据库系统或常用方法冲突。如果坚持使用，请在SQL语句中使用(着重号)引起来：
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17118855090006b9bni.png)

# 3.6 查询常数
SELECT 查询还可以对常数进行查询。对的，就是在 SELECT 查询结果中增加一列固定的常数列。这列的取值是我们指定的，而不是从数据表中动态取出的。
你可能会问为什么我们还要对常数进行查询呢?

SQL 中的 SELECT 语法的确提供了这个功能，一般来说我们只从一个表中查询数据，通常不需要增加一个固定的常数列，但如果我们想整合不同的数据源，用常数列作为这个表的标记，就需要查询常数。

比如说，我们想对 employees 数据表中的员工姓名进行查询，同时增加一列字段corporation，这个字段固定值为“尚硅谷”，可以这样写:![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711885888000lfwqnv.png)

# 四、显示表结构
使用 DESCRIBE 或 DESC 命令，表示表结构。

```sql
DESCRIBE employess; #discribe - 描述
或
DESC employees; #desc - 描述 
```

**显示了表中字段的详细信息**
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17118862690000ck9vg.png)

# 五、过滤数据
想做到的事情：![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711891115000wilbxl.png)
语法：

```sql
delect 字段1,字段2
FROM 表名
WHERE 过滤条件；
```

**WHERE 句子亲随 FROM 子句**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711891380000ujmoyd.png)

