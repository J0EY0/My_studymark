# Mysql

### SQL DB DBMS

DB: DataBase 以文件的形式存在

DBMS : DataBase Management System 数据库管理系统 

SQL：结构化查询语言，是一门标准通用的语言 高级语言 编译由DBMS完成

### 表 TABLE

- 基本存储单元 可读性强
- 行 数据或记录
- 列 字段
- 字段名 数据类型 相关的约束

### SQL语句分类

1. DQL （数据查询语言）：查询语句 select 凡是select 语句都是DQL
2. DML （数据操作语言）：insert delete update 对表中数据的增删改
3. DDL （数据定义语言）：create drop alter 对表结构的增删改
4. TCL（事务控制语言）：commit 提交事务 rollback回滚
5. DCL （数据控制语言）：grant授权 revoke撤销权限

### 导入数据

命令

```
SHOW DATABASES 
```

```
CREATE DATABASE ` `
```

```
USE DATABASE名
```

```
SHOW  TABLES /FROM DATABASE名
```

```
source 路径加文件名
```

```
DROP DATABASE ``
```

### 查看表的结构

```mysql
desc Table名 或  SHOW COLUMNS FROM Table 名
```

### 常用命令

```
SELECT DATABASE()//查看当前使用的数据库
SELECT VERSION()//查看当前版本
exit 退出
```

```
SHOW CREATE TABLE 名 //查看建表语句
```

```mysql
SHOW STATUS/ SHOW GRANTS / SHOW  ERRORS / SHOW WARNINGS
```

分别为 显示服务器的状态信息 显示授权用户 显示服务器错误或警告信息

### 简单查询 --SQL语句

######  格式

```
SELECT `字段名1`，`字段名2`,... FROM `TABLENAME`;
SELECT * FROM `TABLENAME`
```

倘若不想出现重复信息可以使用，但不能部分使用DISTINCT 它应用与所有字段

```mysql
SELECT DISTINCT `字段名`
```

任何一条SQL语句以`；`结尾 且不区分大小写
字段可以参与数学运算

```
SELECT `字段名1`*10 AS '别名' FROM `TABLENAME`;
```

完全限定的表名(有些情况需要使用)

```mysql
SELECT `表名`.`字段名` FROM `数据库名`.`表名`
```

### 条件查询

```mysql
SELECT `字段`，`字段` FROM `TABLENAME` WHERE '条件';
```



```mysql
等于= 大于> 小于< 不等于(<> !=) >= <= AND OR  
BETWEEN...AND(字符串也可以使用)
```

###### 不匹配检查

`<>条件`  找出不是该条件的数据

###### 空值检查

`IS NULL`

！！!注意空值与不匹配

```mysql
SELECT `表名`，`表名` FROM `TABLENAME` WHERE 条件 is NULL/ IS NOT NULL
空不是一个值
```

###### AND 和 OR优先级

```mysq
没有小括号的情况下，先处理AND再处理OR 
```

那么由于AND和OR的处理优先级

会产生一个问题就是执行某些语义下的SQL语句时 会得到不正确的结果

那么除了用()区分优先级以外 还可以用in

in ==or

除此之外

- IN 执行速度一般比OR快
- IN可以包含其他SELECT语句
- 在条件过长的子句中表达更加清晰

```mysql
SELECT `字段`,`字段` FROM `表名` WHERE `字段`IN/not IN ('条件','条件',....)
```



### 模糊查询

###### like

LIKE是谓词而不是操作符

##### 通配符

###### 尾空格可能会干扰通配符的匹配

搜索是可以区分的大小写的

###### `%`

```mysql
表现字符出现的任意次数
但是不能匹配NULL
```

###### `_`

```mysql
只能匹配单字符
```

##### 通配符使用技巧

1. 不要过度使用通配符
2. 除非必要，不要把通配符置于搜索模式的最开始，否则这样搜索速率是最慢的
3. 仔细注意通配符的位置，防止出现错误的结果

```mysql
SELECT `字段` FROM `表名` WHERE `字段` like'%条件%'
举例：_代表第几个位置 找出名字第一个位置为A的字段
如果想要找出字段中包含 '_'的情况，使用'\'' 转义
```

补：多条件模糊查询

```mysql
SELECT `字段` FROM `表名` WHERE CONCAT('','','') LINK '%条件%'
```

### 正则表达式

##### 基本字符匹配

```mysql
RXGEXP
比如 SELECT `字段` FROM	`表名` WHERE RXGEXP "" 
匹配不区分大小写
```

##### 进行OR 匹配

```mysql
SELECT `字段` FROM	`表名` WHERE RXGEXP "|||||" 
```

##### 匹配特定字符

```mysql
SELECT `字段` FROM	`表名` WHERE RXGEXP "[]" 
```

如

```mysql
SELECT `字段` FROM	`表名` WHERE RXGEXP "[123] Ton" 
```

如果数据库中存在该字段

那么会返回

```mysql
1 TON
2 TON
3 TON
```

那么可以看出其跟OR的功能很像

###### 此外还可以设置匹配范围

```mysql
[-]
```

##### 匹配特殊字符

！！！必须以`\\`为前导

```mysql
比如\\. \\-
注：为了匹配反斜杠 需使用 \\\
```

##### 匹配字符类

需要使用时查表即可

![2d0bddaae10e11640e65bdf324caf737.png](https://img-blog.csdnimg.cn/img_convert/2d0bddaae10e11640e65bdf324caf737.png)

[](https://blog.csdn.net/weixin_39760295/article/details/113255230)

##### 匹配多个实例

![1704be3d754d4afc9be71e53e7b331c2.png](https://img-blog.csdnimg.cn/img_convert/1704be3d754d4afc9be71e53e7b331c2.png)

##### 定位符

![c5983cf74f7d267dc79d3b99b02e2001.png](https://img-blog.csdnimg.cn/img_convert/c5983cf74f7d267dc79d3b99b02e2001.png)

`^`有两种用法 在集合中用来否定集合 此处表示文本的开始

那么也可以通过RXGEXP来起到LIKE的作用

```mysql
SELECT `字段` FROM `表名` WHERE RXGEXP "^字段$"
```



### 数据排列

###### ASC 和DESC

```mysql
SELECT `字段` FROM `表名` ORDER BY `字段` ASC/DESC //升序、降序
        2           1       3
ORDER BY最后执行
```

ASC 和DESC只应用与位于其前的字段

### 分组函数

##### 无法直接出现在WHERE 子句当中（未分组） 忽略NULL 一般与group by联合使用（在group by执行结束后执行）

- count 计数 count(*)总记录条数 count(`字段`) 统计字段中不为NULL的数据总数
- sum 求和 
- avg 平均值
- max 最大的数
- min 最小值

###### 对某一组数据进行操作

```mysql
SELECT `分组函数` FROM `表名`
```

<u>**! ! ! 只要数学表达式中有NULL，结果一定为NULL ! ! !**</u>

使用 `ifnull()`函数解决

```
ifnull（`字段`,`想要变为的数据`） 比如 ifnull(c,0) 如果c为NULL看作0处理
```

### 分组查询

- group by 按照某个字段或者某些字段进行分组（WHERE之后执行）<u>**只允许select 后面跟被分组的字段和分组函数**</u>
- having：having是对分组之后的数据进行再次过滤

##### 查询结果去重

distinct 只能出现在所有字段的最前方

```
SELECT distinct `字段名` FROM `表名`
```

### 连接查询

- SQL 92（基本不用） SQL99
- 内连接 等值连接、非等值连接、自连接
- 外连接 左外连接、右外连接
- 全连接 

[笛卡尔乘积现象]([SQL查询中的笛卡尔积现象解决方法 - 十年砍柴MMWS - 博客园 (cnblogs.com)](https://www.cnblogs.com/JackZhangBJ/p/14148564.html))

##### 内连接

###### 能匹配上就查询，匹配不上就不查询了

```mysql
SELECT `字段名` FROM `表名` (INNER可省略)JOIN `表名` ON
```

##### 外连接

###### 返回主表的全部数据，副表匹配不上就返回NULL

```mysql
SELECT `字段名`FROM `表名` LEFT / RIGHT (OUTER) JOIN `表名` ON
```

补：三张表以上的连接查询

```mysql
SELECT `字段名`FROM `表名` LEFT / RIGHT (OUTER) JOIN `表名` JOIN `表名` ……
```

#### WHERE 嵌套子查询

```mysql
SELECT `字段名`FROM WHERE(SELECT 。。。。)
```

#### FROM 嵌套子查询

```mysql
SELECT `字段名`FROM （。。。。） `表名` 。。。 
```

#### SELECT 嵌套子查询

```mysql
SELECT `字段名` (......) FROM ....
```

#### Union用法

连接 

```mysql
SELECT `字段名` (......) FROM UNION SELECT `字段名` (......) FROM ....
```

#### Limit

mysql特有 取结果集中的部分数据

```mysql
SELECT `字段名`  FROM `表名`  LIMIT 次数
```

如果要求从特定行开始

```mysql
SELECT `字段名` FROM `表名` LIMIT 行数,次数
```

###### 注:

​	如果分页查询的总次数不够，如一共有19条数据，分为两页，每页十个数据，那么查询最后一页时，只会返回9条

为了避免产生歧义

Mysql5支持LIMIT的另外一种替代语法

```mysql
SELECT `字段名` FROM `表名` LIMIT  次数 OFFSET行数
```

