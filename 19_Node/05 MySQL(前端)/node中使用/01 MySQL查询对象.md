先需要知道，当使用mysql查询得到的数据的时候，在 Navicat 中看着是一个表，但是在网络中使用的时候是个数组，数组里面有对象，每一个对象对应一行 MySQL 查询得到数据。

```sql
INSERT INTO songs_db VALUES("axl", 18);
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1767093479000ti66wk.png)

在使用这个查询到的数据的时候的格式如下(对象数组)：

```json
[
	{
	  name: "axl",
	  age: "18"
	},
	{
	  name: "cba",
	  age: "22"
	}
]
```

但是我们在真实中的数据会很复杂，会是对象嵌套对象，例如：

```json
[
  {
    name: "axl",
    age: "18",
    friends: [
      {
        name: "cba",
        age: "22"
      }
    ]
  }
]
```

> [!tip]
> SQL 查询得到的数据，默认是不会进行这种嵌套，需要使用到 [[13 MySQL 数据类型#十一、JSON 类型|JSON]] 的类型。

案例：要用 JSON_OBJECT;

```sql
SELECT
	products.id AS id,
	products.title AS title,
	products.price AS price,
	products.score AS score,
	JSON_OBJECT( 'id', brand.id, 'name', brand.name, 'rank', brand.phoneRank, 'website', brand.website ) AS brand 
FROM products
LEFT JOIN brand 
ON products.brand_id = brand.id;
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1767093822000j4lkox.png)

