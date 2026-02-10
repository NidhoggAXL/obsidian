# 一、认识mysql2库

前面所有的操作都是在GUI工具中，通过执行SQL语句来获取结果的，那真实开发中肯定是通过代码来完成所有的操作的。

那么如何可以在Node的代码中执行SQL语句来，这里我们可以借助于两个库：

 - **mysql**：最早的Node连接MySQL的数据库驱动；
 - **mysql2**：在mysql的基础之上，进行了很多的优化、改进；

目前相对来说，更偏向于使用mysql2，mysql2兼容mysql的API，并且提供了一些附加功能

 - **更快/更好的性能**；
 - **Prepared Statement（预编译语句）**：
	 - 提高性能：将创建的语句模块发送给MySQL，然后MySQL编译（解析、优化、转换）语句模块，并且存储它但是不执行，之后我们在真正执行时会给提供实际的参数才会执行；就算多次执行，也只会编译一次，所以性能是更高的；
	 - 防止SQL注入：之后传入的值不会像模块引擎那样就编译，那么一些SQL注入的内容不会被执行；or 1 = 1不会被执行；
 - **支持Promise**，所以我们可以使用async和await语法
 - 等等....

# 二、基本使用

安装 mysql2 ：

```bash
npm install mysql2
```

mysql2的使用过程如下：

 - 第一步：创建连接（通过createConnection），并且获取连接对象；
 - 第二步：执行SQL语句即可（通过query）；

```js
const mysql = require("mysql2");

// 1.创建链接（链接数据库）
const connection = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "yrm1999.1203",
  database: "music_db",
});

// 2.编写sql语句 statement-陈述
const statement = "SELECT * FROM songs_db;";

// 3.执行sql语句
// err(错误信息) values(查询结果) fileds(字段信息)
connection.query(statement, (err, values, fileds) => {
  if (err) {
    console.log(err);
    return;
  }
  console.log(values);
  //[ { name: 'axl', age: 18 }, { name: 'cba', age: 22 } ]
});

```

和 MySQL 创建连接后，要进行断开，断开有两种方式，下面两种有什么区别呢？

```js
connection.end()
connection.destroy()
```

1. `connection.end()`：
    
    - 这是一个优雅的关闭方式
    - 会等待所有正在执行的查询完成后才关闭连接
    - 会发送一个`COM_QUIT`数据包到MySQL服务器
    - 保证数据的完整性
    - 因此能正确返回结果
	
2. `connection.destroy()`：
    
    - 这是一个强制关闭方式
    - 会立即终止连接，不等待正在执行的查询
    - 不会发送任何数据包到MySQL服务器
    - 可能导致数据丢失或不完整
    - 因为是强制关闭，所以可能会导致查询结果返回undefined

> [!tip] 开发中选择：
> - 如果需要确保数据完整性，使用`connection.end()`
> - 只有在紧急情况下或确定没有重要查询执行时，才使用`connection.destroy()`
> - 对于生产环境，推荐使用连接池（connection pool）来管理连接，这样可以更好地处理连接的生命周期

# 三、预编译语言

Prepared Statement（预编译语句）：

 - 提高性能：将创建的语句模块发送给MySQL，然后MySQL编译（解析、优化、转换）语句模块，并且存储它但是不执行，之后真正执行时会给?提供实际的参数才会执行；就算多次执行，也只会编译一次，所以性能是更高的；
 - 防止SQL注入：之后传入的值不会像模块引擎那样就编译，那么一些SQL注入的内容不会被执行；`or 1 = 1` 不会被执行；

```js
const mysql = require("mysql2");

// 1.创建链接（链接数据库）
const connection = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "yrm1999.1203",
  database: "music_db",
});

// 2.编写sql预处理语句
const statement = "SELECT * FROM songs_db WHERE name = ? AND age > ?";

// 3.执行sql预处理语句
connection.execute(statement, ["axl", 17], (err, results) => {
  console.log(results)
  //[ { name: 'axl', age: 18 } ]
})
```

# 四、连接池

Connection Pools（连接池）：

前面是创建了一个连接（connection），但是如果我们有多个请求的话，该连接很有可能正在被占用，那么我们是否需要 每次一个请求都去创建一个新的连接呢？ 

- 事实上，mysql2给我们提供了连接池（connection pools）； 
- 连接池可以在需要的时候自动创建连接，并且创建的连接不会被销毁，会放到连接池中，后续可以继续使用； 
- 我们可以在创建连接池的时候设置LIMIT，也就是最大创建个数；

```js
const mysql = require("mysql2");

// 1.创建链接（链接数据库）
const connection = mysql.createPool({
  host: "localhost",
  user: "root",
  password: "yrm1999.1203",
  database: "music_db",
  connectionLimit: 3//最多连接的数量
});

// 2.编写sql预处理语句
const statement = "SELECT * FROM songs_db WHERE name = ? AND age > ?";

// 3.执行sql预处理语句
connection.execute(statement, ["axl", 17], (err, results) => {
  console.log(results)
  //[ { name: 'axl', age: 18 } ]
})

// 4.关闭连接
connection.end();
// connection.destroy()
```

# 五、Promise方式

目前在JavaScript开发中我们更习惯Promise和await、async的方式，mysql2同样是支持的：

```js
const mysql = require("mysql2");

// 1.创建链接（链接数据库）
const connection = mysql.createPool({
  host: "localhost",
  user: "root",
  password: "yrm1999.1203",
  database: "music_db",
  connectionLimit: 3
  //最多连接的数量
});

// 2.编写sql预处理语句
const statement = "SELECT * FROM songs_db WHERE name = ? AND age > ?";

// 3.执行sql预处理语句（使用Promise方式）
connection.promise().execute(statement, ["axl", 16]).then((res) => {
  const [values, fileds] = res
  console.log(values)
})

```

# 六、获取连接是否成功

```js
const mysql = require("mysql2");

// 创建连接池
const pool = mysql.createPool({
  host: "localhost",
  port: 3306,
  user: "root",
  password: "yrm1999.1203",
  database: "xlhub",
  connectionLimit: 5,
});

// 获取连接是否成功
pool.getConnection((err, connection) => {
  if (err) {
    console.log("数据库连接失败", err);
    return
  } 

  // 测试连接
  connection.connect(err => {
    if (err) {
      console.log("数据库连接失败", err);
      return
    } else {
      console.log("数据库连接成功")
    }
  })
});

// 获取连接对象（promise）
const connection = pool.promise();

module.exports = connection;

```