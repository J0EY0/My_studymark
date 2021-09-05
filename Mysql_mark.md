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

##### 关于count(`字段`) 、count(`1`)、  count(`*`)这三者之间的差别

```mysql
执行效果上：
count(*)包括了所有的列，相当于行数，在统计结果的时候，不会忽略列值为NULL。
count(1)包括了忽略所有列，用1代表代码行，在统计结果的时候，不会忽略列值为NULL 。
count(列名)只包括列名那一列，在统计结果的时候，会忽略列值为空（这里的空不是只空字符串或者0，而是表示null）的计数，即某个字段值为NULL时，不统计。
执行效率上：

列名为主键，count(列名)会比count(1)快。
列名不为主键，count(1)会比count(列名)快。
如果表多个列并且没有主键，则 count（1） 的执行效率优于 count（*）。
如果有主键，则 select count（主键）的执行效率是最优的。
如果表只有一个字段，则 select count（*）最优。
```

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

```mysql
ifnull（`字段`,`想要变为的数据`） 比如 ifnull(c,0) 如果c为NULL看作0处理
```

### 分组查询

- group by 按照某个字段或者某些字段进行分组（WHERE之后执行）<u>**只允许select 后面跟被分组的字段和分组函数**</u>
- having：having是对分组之后的数据进行再次过滤
- having支持所有的WHERE操作符 WHERE过滤行 HAVING过滤分组

##### 查询结果去重

distinct 只能出现在所有字段的最前方

distinct只能用于COUNT(字段)如果用于COUNT(*)则会发生错误

```mysql
SELECT distinct `字段名` FROM `表名`
```

### 连接查询

- SQL 92（基本不用） SQL99
- 内连接 等值连接、非等值连接、自连接
- 外连接 左外连接、右外连接
- 全连接 
- 自然连接

[笛卡尔乘积现象]([SQL查询中的笛卡尔积现象解决方法 - 十年砍柴MMWS - 博客园 (cnblogs.com)](https://www.cnblogs.com/JackZhangBJ/p/14148564.html))

##### 内连接

使用内连接替代子查询

虽然最终结果相同

但是内连接的执行效率较比于子查询要快很多

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

##### 自然连接

排除多次出现 每个列只返回一次

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

#### 创建计算字段

计算字段基本不存在于数据库表中

##### 拼接字段

--将值连结到一起

###### Concat()函数

``` mysql
SELECT Concat(`字段`,....) FROM `表名`
```

###### RTrim()函数

```mysql
去除值右边的所有空格
```

###### LTrim()函数

```mysql
去除值左边的所有空格
```

#####  使用别名(导出列)

###### AS 

as其实可以省略，但是为了可读性，最好不要省略

```mysql
SELECT Concat(`字段`,....) AS `字段` FROM `表名` 
```

 返回当前时间

```mysql
SELCET NOW()
```

#### 使用数据处理函数

###### Upper()函数

upper函数可以将字符串转为大写

```mysql
SELECT Upper('abc')
output:
ABC
```

##### 常用文本处理函数

```mysql
Left()   #返回串左边字符
Right()  #返回串右边字符
Length() #返回串的长度
Locate() #找出串的一个字串
Lower()  #将串转换为小写
Upper()  #将串转换为大写
LTrim()  #去除串左边的空格
RTrim()  #去除串右边的空格
Soundex()#返回串的Soundex值
SubString()#返回字串的字符
```

###### Soundex

其是一个将任何字符串转换为描述其语音表示的字母数字模式算法 使其能够对串进行发音比较而不是字母比较

##### 日期和时间处理函数

```mysql
NOW()-------------------------------系统当前的日期时间
Year()------------------------------返回一个日期的年份部分
Month()-----------------------------返回一个日期的月份部分
Date() -----------------------------返回日期时间的日期部分
Day() ------------------------------返回一个人日期的天数部分
Dayofweek()-------------------------返回一个日期对应的星期部分
Hour() -----------------------------返回一个时间的小时部分
Minute()----------------------------返回一个时间的分钟部分
Second()----------------------------返回一个时间的秒部分
CurTime()---------------------------返回当前的时间
CurDate()---------------------------返回当前日期
Day-format()------------------------返回一个格式化的日期时间字符串
AddDate()---------------------------增加一个日期（天，周等）
AddTime()---------------------------增加一个时间（时，分等）
DateDiff()--------------------------计算两个日期之差
Date_add()--------------------------高度灵活的日期运算函数
```

首选日期格式：`yyyy-mm-dd`

最好使用四位数的年份

##### 如果需要日期

###### 使用Date()

##### 如果需要时间

###### 使用Time()

##### 数值处理函数

![img](https://img-blog.csdnimg.cn/20190908112019431.png)

#### 子查询

格式化SQL 包含子查询的SELECT 语句是难以阅读并加以调试的

所以对子查询应该进行分行处理

#我的理解：子查询就是SELECT等等语句的嵌套 当具备复杂语义逻辑查询时，使用子查询先创建一个符合上一层SELECT表结构，再通过上一层的SELECT完成查询

###### 相关子查询

只要列名有多义性 就要使用相关子查询

子查询最常见的用例是在WHERE子句的IN操作符中

#### 联结表

表联结的越多，性能下降越厉害

#### 组合查询

Mysql允许执行多个查询，并将结果作为单个查询结果集返回
查询通常称为并或者组合查询

###### 使用组合查询的两种情况

- 单个查询从不同表中返回类似结构的数据
- 对单个表执行多次查询 按单个查询返回数据

使用**Union**进行组合查询

从组合查询的两种情况可以分析出 任何具有多个WHERE 子句的SELECT语句都可以看作是组合查询

##### UNION规则

- 必须由两条或者两条以上的UNION语句组合而成 每个SELECT语句之间必须由UNION分割

- UNION的每个查询必须包含相同的列、表达式或者聚集函数

- 列数据类型必须兼容

  <u>Union会自动去除重复的行</u>

  那么跟使用多个WHERE 子句嵌套一样

  如果要返回所有行 使用**UNION ALL** 而不是**UNION**

  当然 **ORDER BY** 也只能出现一次 那么在UNION中会自动对所有SELECT 语句生效

#### 全文本搜索

Mysql 中较为常用的两个引擎

- MyISAM
- InnoDB

前者支持全文本搜索而后者不支持

那么如何启用全文本搜索支持呢

只需要在创建表的时候启用全文本搜索

一般在创建表的时候使用FULLTEXT语句

它给出索引列一个被逗号分隔的列表

```mysql
CREATE TABLE `XXXX`(
	`xxx` INT NOT NULL AUTO_INCREMENT,
    `xx`  VARCHAR(20) NOT NULL,
    PRIMARY KEY(`xxx`)
    FULLTEXT(`xx`)
)ENGINE =MyISAM;
```

##### **<u>！！注意！！</u>**

不要在导入数据到一个新表时，使用FULLTEXT() 否则对性能有影响

而是应该在数据导入完成后通过ALTER修改表的属性

##### 进行全文本搜索

使用MATCH() 以及Against()函数

match指定搜索的列

against指定搜索的表达式

example:

```mysql
SELECT `note_text` FROM productnotes WHERE Match(`note_text`) Against('rabbit');
```

意为 从productnotes表中的note_text列搜索所有包含rabbit字段的结果

###### 传递给Match()的值必须要跟FULLTEXT()定义的字段相同

###### 除非以二进制的方式搜索 否则搜索不区分大小写

##### 查询扩展

```mysql
SELECT `note_text` FROM productnotes WHERE Match(`note_text`) Against('rabbit' WITH QUERY EXPANSION);
```

##### 布尔文本搜索

```mysql
SELECT `note_text` FROM productnotes WHERE Match(`note_text`) Against('rabbit' IN BOOLEAN MODE);
```

以上语句没有使用布尔操作符 其结果跟没使用布尔操作符相同

example：

查询出有rabbit 但不包含rope的文本

```mysql
SELECT `note_text` FROM productnotes WHERE Match(`note_text`) Against('rabbit -rope*' IN BOOLEAN MODE); #mysql 4.x 使用此句会有问题 应该把*去掉
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200924095936756.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTk4NDA0NA==,size_16,color_FFFFFF,t_70#pic_center)

<u>在布尔方式中 不按等级值降序排序返回的行</u>

使用说明：

- 3个或3个字符一下的词被定义为短词 而短词一般会被忽略 当然阈值可以自己设置
- Mysql 有一个内建非用词的列表 这些词在全文本索引时常常被忽略
- 许多词出现的频率很高 Mysql规定出现概率大于50%的词 会被忽略
- 如果表中的行数小于3 则全文本搜索不返回结果
- 忽略语句中的单引号
- 不具有词分隔符比如中文不能恰当的返回结果
- 仅在MyISAM中支持全文本搜索 

#### 插入数据

##### INSERT (一般不会产生输出)

```mysql
INSERT INTO `表名` VALUES(`列名`,`列名`,`列名`,`列名`)
```

但是这种语法虽然简便 却不安全

可以发现其高度依赖于表的结构顺序 如果当表的结构发生变化 就会出现问题

使用以下更安全 但更加繁琐的方式插入数据

```mysql
INSERT INTO `表名` (`列名`,`列名`,`列名`,`列名`)VALUES(值,值,值,值)
```

##### 仔细给出值

必须给出VALUES的正确数目 

使用第二种语法还可以在表结构允许的情况下

##### 提高整体性能

```mysql
数据库经常被多个用户访问
INSERT操作可能非常耗时
如果SELECT即查询功能最为重要 那么可以在INSERT INTO 之中加入LOW_PRIORITY
指示mysql降低insert语句的优先级
```

##### 插入多个行

```mysql
INSERT INTO `表名` (`列名`,`列名`,`列名`,`列名`)VALUES(值,值,值,值),(值,值,值,值)
```

即单条INSERT语句有多组值 每组值用圆括号括起来用逗号分隔

##### 使用单条INSERT语句插入多个行比使用多个INSERT可以提升INSERT的性能

##### 插入检索数据

```mysql
INSERT INTO `表名` (`列名`,`列名`,`列名`,`列名`)  SELECT `列名`,`列名`,`列名`,`列名` FROM `表名`
```

##### 更新和删除数据

为了更新(修改)表中的数据

可以使用Update语句

- 更新所有行
- 更新指定行

```mysql
UPDATE `表名` 
SET `列名`='xxxx'
WHERE XXXX
```

这就是UPDATE使用的基本格式

如果使用update更新多行时，如果不想使其中的一次update报错导致整个update语句失效可以使用IGNORE

```mysql
UPDATE IGNORE `表名`
```

在表结构允许的情况下 可以通过将列值置为NULL来删除值

为了删除数据

可以使用Delete语句

而delete语句更加简单

它直接删除一行

```mysql
DELETE FROM `表名`WHERE XXXX
```

delete是删除表里面的值 而不是表本身

要删除整张表需要使用drop

```mysql
DROP Table ``
```

而要删除整张表中的值

为了性能考虑 应该使用TRUNCATE函数

它是在删除原来的表之后重新建一张新表

- 除非打算更新或删除 否则不要使用 update或者delete 不携带where条件
- 保证每个表都有主键
- 应该先用SELECT测试
- 使用强制实施引用完整性的数据库，则有mysql将不会允许删除与其他表有关联的行

Mysql 没有undo，所以对待这两个语句需要谨慎使用

#### 创建和操纵表

```mysql
CREATE TABLE `表名`(
)
```

#### NULL值

null值就是没有值或者缺值

```mysql
#对于建表这一过程而言 尽量使用NOT NULL去约束
#而不是NULL 尽管 NOT NULL对于NULL来说提升性能很小 但是可以避免一些意想不到的错误 

```

##### 理解NULL和空串的区别

NULL是空值即没有值 而空串即`''`它在NOT NULL中是允许的

##### 主键只允许使用不为NULL值的列



##### AUTO_INCREMENT

使用Mysql提供的auto_increment字段 可以实现自增类型

但是有一缺点就是无法确定mysql生成的值

可以使用last_insert_id() 函数获取这个值

一张表只能拥有一个auto_increment

```mysql
SELECT last_insert_id() 
```

##### Default

在创建表时 可以使用Default为字段赋予初值

##### 引擎

在创建表的过程中 我们可以通过

```mysql
CREATE TABLE `表名`(
	xxx
	xxx
    xxx

)ENGINE='';
```

来指定引擎

不同的引擎有不同的有点和特性

- InnoDB 是一个可靠的事务处理引擎 不支持全文本搜索
- MEMORY等同于MyISAM 但是当数据存储在内存中而不是磁盘时 速度会特别快 常用于创建临时表
- MyISAM 一个性能很高的搜索引擎 支持全文本搜索

引擎可以混用

<u>但是注意外键不能跨引擎</u>

##### 更新表

<u>ALTER</u>

修改表名

```mysql
ALTER TABLE `` RENAME TO``;
```

修改表注释

```mysql
ALTER TABLE `` COMMENT;
```

修改字段类型和注释

```mysql
ALTER TBALE `` modify COLUMN `` xxx COMMENT '';
```

增加一个字段

```mysql
ALTER TBALE `` ADD `` xxx;
```

修改字段名字 需要指定类型等

```mysql
ALTER TABLE `` CHANGE `` ``xxx;
```

删除字段

```mysql
ALTER TABLE `` DROP ``;
```

在某个字段后增加字段

```mysql
ALTER TABLE `` ADD COLUMN `` xxx AFTER ``;
```

调整字段顺序

```mysql
ALTER TABLE `` CHANGE `旧字段名` `新字段名` xxx AFTER ``;
```

使用ALTER TABLE 时应该小心 数据被误删除

##### 删除表

```mysql
DROP TABLE ``
```

重命名表

```mysql
RENAME TABLE `` TO ``
```

#### 使用视图

<u>需要Mysql5以上</u>

视图本身不包含数据 每次使用视图时必须处理查询执行时所需的任一个检索

如果使用多个联结和过滤创建了复杂的视图或者嵌套了视图 性能会下降的很厉害

##### 为什么要使用视图

- 重用SQL语句
- 简化复杂SQL操作
- 使用表的组成部分而不是整个表
- 保护数据
- 更改数据格式和表示

##### 使用规则

- 与表一样 视图的名字必须唯一
- 对于创建的视图没有数量限制
- 视图可以嵌套
- ORDER BY 可以用在视图中
- 视图不能索引 也不能有相关联的触发器和默认值
- 视图可以与表一起使用

#####  创建视图

``` mysql
CREATE VIEW `viewname`
```

##### 查看视图

```mysql
SHOW CREATE VIEW `viewname`
```

删除视图

```mysql
DROP VIEW `viewname`
```

更新视图

```mysql
1. DROP VIEW `viewname` / CREATE VIEW `viewname`
2. CREATE OR REPLACE VIEW `viewname`
```

##### example:

```mysql
CREATE VIEW `example` AS
SELECT *FROM `xxx`,`xxx` 
WHERE XXXX;
```

如果在视图查询中使用了另外的WHERE子句 那么两个子句会自动合并

一般的 应该将视图应用于检索 而不是更新

#### 存储过程

使用以下语句来创建一个存储过程

```mysql
CREATE
	[DEFINER={user|CURRENT_USER}]
PROCEDURE `名字`([proc_parameter[,....]])
	[characteristic ...] routine_body
	
proc_parameter:
	[IN|OUT|INOUT] param_name type #输入、输出、输入输出
	
characteristic:
	COMMENT 'string'
	| LANGUAGE SQL
	|[NOT] DETERMINISTIC
	|{CONTAINS SQL | NO SQL| READS SQL DATA| MODIFIES SQL DATA}
	|SQL SECUITY {DEFINER |INVOKER}

routine_body:
	Valid SQL routine statement
[begin_label: BEGIN]
	[statement_list]
	...
END [end_label]
```

如果使用MYSQL命令行进行存储 那么

可以使用

```mysql
DELIMITER 符号
```

自定义语句结束的表示符号

##### 删除

```mysql
DROP PROCEDURE `name`	
```

仅当存在时删除

```mysql
DROP PROCEDURE IF EXISTS
```

##### 变量名

```mysql
所有的mysql变量名必须由@开头
由 DECLARE 创建
```

##### 调用

使用以下语句调用

```mysql
CALL `函数名`
```

##### 注释

在存储过程中有两种注释风格

```mysql
1. --
2. // #语言风格 常用于多行注释
```

#### 游标

游标只用于存储过程

##### 创建游标

```mysql
在创建存储过程的时候 使用DELCARE 定义游标
CREATE PROCEDURE `xx`(IN XXX INTEGER)
BEGIN
	XXXX
	XXXX
	XXXX
    DECLARE `XXX` CURSOR
    FOR 
    SELCET xxxx
END
```

##### 打开或者关闭游标

使用以下语句打开游标

```mysql
OPEN `CURSOR`
```

使用以下语句关闭游标

当然你也可以选择不关闭他 那么游标会在存储过程END语句后自动关闭

```mysql
CLOSE `CURSOR`
```

#####  使用游标 

那么当一个游标被打开后 可以使用Fetch语句调用

```mysql
FETCH `游标` INTO xx
```

可以理解成一个指针 在读取数据 每读取一行就往下移动

#### 触发器

触发器是MYSQL响应

- DELETE
- UPDATE
- INSERT

这三个语句(或者任何位于BEGIN 和END之间)而自动执行的一条SQL语句

它支持表 不支持视图或者临时表

##### 创建触发器

- 唯一的触发器名
- 触发器关联的表
- 触发器应该响应的活动
- 触发器何时执行

使用以下语句创建触发器

```mysql
CREATE TRIGGER `名`	BEFORE/ AFTER DELETE/ UPDATE/ INSERT xxx 
```

 触发器中不支持CALL语句
