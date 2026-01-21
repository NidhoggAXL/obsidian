在多对多关系中，我们希望查询到的是一个数组：

 - 比如一个学生的多门课程信息，应该是放到一个数组中的；
 - 数组中存放的是课程信息的一个个对象；
 - 这个时候我们要 JSON_ARRAYAGG 和 JSON_OBJECT 结合来使用；

```sql
SELECT
	stu.id,
	stu.NAME,
	stu.age,
	JSON_ARRAYAGG(
	JSON_OBJECT( 'id', cs.id, 'name', cs.NAME )) AS courses 
FROM
	students stu
	LEFT JOIN students_select_courses ssc ON stu.id = ssc.student_id
	LEFT JOIN courses cs ON ssc.course_id = cs.id 
GROUP BY
	stu.id;
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17670945980006mr2ps.png)
