---
title: "mysql中count(name)和count(*)的区别是什么"
date: 2024-07-31
---
这篇文章让我们看看MySQL中`count(*)`和`count(column_name)`有什么区别。也许你知道它们都是计算结果行数的，那么在使用的时候如何选择呢。

![image.png](https://note-1251668647.cos.ap-nanjing.myqcloud.com/20240731225646.png)


我在MySQL库中创建了一个`t_hero`表

```mysql
CREATE TABLE `t_hero` (
  `id` int NOT NULL,
  `name` char(10) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
```

往表里插入了6条数据，如下
![image.png](https://note-1251668647.cos.ap-nanjing.myqcloud.com/20240731224311.png)

然后使用`count(*)`、`count(distinct column)`和`count(column)`查询

```mysql
SELECT COUNT(*), 'COUNT(*) ' FROM t_hero
UNION
SELECT COUNT(name), 'COUNT(name)' from t_hero
UNION
SELECT COUNT(DISTINCT name), 'COUNT(DISTINCT name)'from t_hero;
```

输出结果

```
6	COUNT(*) 
5	COUNT(name)
4	COUNT(DISTINCT name)
```

因此，可以得出结论：

- 要计算查询返回的行数，请执行以下操作：
  `select count(*) from table;`
- 计算查询返回的非 null 值的数量：  
  `select count(column) from table;`
- 计算查询返回的不同值的数量：  
  `select count(distinct column) from table;`
