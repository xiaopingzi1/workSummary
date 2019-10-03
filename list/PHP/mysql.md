# 1. MySQL数据库服务器

##  1.1 什么是数据库

存储数据的仓库。

常见的数据库: MySQL、 Oracle、 Sqlserver、 DB2等。



##  1.2 MySQL简介

MySQL是一个关系型数据库管理系统，由瑞典MySQL AB 公司开发，目前属于 Oracle 旗下产品 

在一个MySQL服务器中有多个数据库，每个数据库又有多个数据表。 数据是存储在数据表当中的。

数据表的结构和excel一模一样
表结构:  

   和excel表的结构是一样的。
   每一列都是一类数据 --- 字段
   每一行代表一条数据 --- 记录

 

##  1.3 安装客户端

MySQL是一款C/S结构的软件。

MySQL本身是服务器端。  phpStudy中的MySQL是服务器端

常见的客户端: CMD 、 Navicat、 Sqlyog、 phpmyadmin等等

 

# 2. 创建/删除数据库

操作数据库需要使用SQL语句（结构化查询语言）

1) 创建数据库

    语法格式: create database 库名;
    
    示例：create database study；   创建一个名为 study的数据库
    	 create database cms；     创建一个名为 cms 的数据库


2) 删除数据库:

  语法格式:  drop database 库名;

  示例:     drop database school;  删除school库

		drop database cms;      删除cms库



# 3. 创建数据表

## 3.1 创建表的基本格式

语句格式:

CREATE TABLE 表名 (
       列名     数据类型(长度)    完整性约束条件,
       列名     数据类型(长度)    完整性约束条件,
       ......
) engine=myisam default charset=utf8

 

==注意事项:==
   ==列名、数据类型、长度是必有的； 完整性约束条件可以没有==
   ==最后的 utf8 没有 -==




# 4. 数据类型和完整性约束条件

## 4.1 数据类型

1) 整型:   int

    tinyint（微整型 -128 ~~ 127）  
    int(整型 -2,147,483,648  ~~ 2,147,483,647)



 1) 字符串:

     varchar: 可变长度  varchar(30)    存储abc，varchar会占用3位长度
     char: 固定长度     char(30)    存储abc，char会占用30位长度
     char的执行速度比varchar快，所以能用char就用char



2) 枚举:  enum （单选）  /   集合: set（多选）

    enum(‘男’, ‘女’)   
    enum(‘武侠’, ‘玄幻’, ‘恐怖’, ‘都市言情’)
    
    set('古装','喜剧','警匪','恐怖','穿越','动作')
    set('吃', '喝', '玩', '乐')



3) 日期:  

    date :   年-月-日
    datetime :  年-月-日  时:分:秒
    time： 时:分:秒
    int: 存储时间戳



4) 文本: text  大文本   （文章正文，商品详情等内容比较多的数据都选用text类型）



## 4.2 完整性约束条件

 完整性约束条件，就是进一步限制字段中保存的数据

1) unsigned: 无符号，只用在整型字段上。

   tinyint unsigned  无符号微整型 0~~255 

   int unsigned  0~~42亿

2) auto_increment: 自增长，只用在整型字段上。 

3) primary key: 主键。 

    作用: 用来标志唯一一行数据的。
    特点: 唯一 、 非空 、经常和auto_increment结合使用。 主键和自增长配合就能确定唯一的一条数据了。 主键一般都会选择整型字段。

4) unique: 唯一。 该列中不能出现重复值

5) not null: 非空。 该列中不能有 NULL 数据。	




# 5. **数据查询**

语法格式: 

SELECT  字段名1, 字段名2, ......

  FROM 表名	

      [ WHERE <条件表达式> ]
    
      [ ORDER BY <字段名> [ ASC|DESC ]]
    
      [ LIMIT  START, LENGTH] 

 




## 5.1 基本查询

格式:  select  字段名1, 字段名2,....  from  表名 

## 5.2 带where子句的查询

select  field1, field2... from 表名  查询表中的所有数据

  where 可以使用条件来筛选查询出的结果


## 53 in关键词

集合:  一组相同类型的数据，使用()来包含，括号内使用 ， 分隔开

(1, 2, 3, 4, 5)  (‘潮科技’, ‘会生活’, ‘奇趣事’, ‘美奇迹’)  

 
## 5.4 模糊查询

通配符:

  %: 代表任意长度(包括0)的任意字符

  _:  代表1位长度的任意字符

    a%b :  ab  abb  a对萨达b
    a_b: acb  atb  
    a_b%:  acb  a&baaad

like: 在执行模糊查询时，必须使用like来作为匹配条件



## 5.5 order by 排序

order by 可以对查询结果按某个字段的升降进行排序

  升序 asc （默认值） ，  降序 desc 

可进行排序的字段通常是  整型  英文字符串型  日期型  (中文字符串也行,但一般不用)



 

## 5.6 limit 限制

limit用来限制查询结果的起始点和长度

 格式:  limit  var1, var2

 var1: 起始点。 查询结果的索引，从0开始。 0代表第一条数据

 var2: 长度



limit 通常用于分页查询：

   第一页: select  *  from ali_admin  limit 0,3

   第二页: select  *  from ali_admin  limit 3,3

   第三页: select  *  from ali_admin  limit 6,3





# 6. 关系型数据库


使用多张数据表联合保存数据。

 核心重点： 字段的对应关系

 sc表中的 sno要和  student表中的sno对应，sc.sno的值一定要存在于 student.sno

 sc表中的 cno 要和 course表中的cno对应，sc.cno的值一定要存在于course.cno

缺点: 表多
优点:
   数据耦合性低
   每个数据表都能够独立管理


# 7. 多表查询

关键词: join ..  on ..

 

格式:  

select  *  from  表1

  join 表2  on  链接条件

链接条件一定是   表1的某个字段 =  表2的某个字段



目标: 查询学生的基本信息，但要显示系名而不是系号

表:  student (学生基本信息) 、 dept(系名)

字段： sno、sname、sage、dname

链接条件：  student.dno=dept.dno

流程：

   ① 确定要查询哪些表

   ② 确定查询哪些字段

   ③ 确定链接关系

   ④ 确定哪个是表1，哪个是表2

   ⑤ 筛选

   ⑥ 排序

​    ⑦ 限制



 

# 8. 添加数据

格式:  insert into 表名(字段名1，字段名2,....)  values(值1，值2，....)

 注意: ==字段的顺序要和值的顺序是完全匹配的==
          ==自增长类型的主键，可以使用null来填充；MySQL会自动填充数据==
          ==如果每个字段都有数据，那么表名后面可以不跟字段名，但是values里面的顺序必须正确==

 
因为添加所有数据，所以表名(ali_cate)之后没有写字段名

使用null来设置自增长的字段(cate_id)

# 9. 修改数据

格式:  

  update  表名   set   字段1=值1, 字段2=值2,...  where  修改条件

  修改表中的哪一条（几条）数据的 字段1=值1...

 

# 10. **删除数据**

格式:  delete from 表名  where 删除条件


# 11. PHP操作MySQL

PHP操作MySQL有三组常见的函数： mysql   ==mysqli==  pdo



1) 链接MySQL服务器  

2) 选择要操作的数据库

3) 设置字符集 （不设置字符集可能会出现乱码问题）

4) 执行SQL语句

5) 处理SQL执行结果

6) 关闭MySQL链接

除了第五步，其他每一步都是固定的，对应一个mysqli的函数



 

1) 链接MySQL服务器 --- mysqli_connect(var1, var2, var3)

  参数1: MySQL数据库的主机地址
  参数2: 用户名
  参数3: 用户名对应的密码
  返回值: 数据库链接资源

  `$conn = mysqli_connect('localhost', 'root', 'root');`

 

2) 选择要操作的数据库  --- mysqli_select_db(var1, var2)

  参数1: 数据库链接资源
  参数2: 数据库名称

 `mysqli_select_db($conn, 'demo');`

 

3) 设置字符集 --- mysqli_query(var1, var2)

  参数1: 数据库链接资源
  参数2: sql 语句 ----  set names utf8  (设置字符集的sql语句)

  `mysqli_query($conn, 'set names utf8'); `



4) 执行SQL语句 --- mysqli_query(var1, var2)

  参数1: 数据库链接资源
  参数2: sql 语句 ----  增删改查SQL语句
  返回值: 如果是查询，则返回结果对象，该对象里面包含了从数据表中取出的数据
                如果是增删改，则返回布尔值，执行成功返回true，失败返回false

  `$result = mysqli_query($conn, $sql); `



5) 处理**==查询结果==**

  **==mysqli_fetch_assoc(var);==**

  参数: 查询结果对象
  返回值: 一维数组，下标是数据表字段

  将当前行的数据取出并返回成一维数组，同时将指针向下移动一行。
  如果已经无法返回一维数组时，则返回false 



6) 关闭MySQL链接资源 --- mysqli_close(var)

   参数: 数据库链接资源




# 12. mysql 函数组

## 12.1 mysql函数组操作数据库

  mysql函数组的用法和mysqli的用法一样，只是参数略有不同。

  1) 链接MySQL服务器 --- mysql_connect()

  2) 选择数据库  ---  mysql_select_db()

  3) 设置字符集 --- mysql_query('set names utf8')

  4) 执行SQL语句  ---  mysql_query()

  5) 处理SQL执行结果

  6) 关闭链接资源  --- mysql_close()


## 12.2 其他相关函数

```
array mysql_fetch_row($resource)     功能同mysql_fetch_assoc，但取出的索引数组
array mysql_fetch_array($resource)   功能同mysql_fetch_assoc，但取出关联和索引的混合数组

int  mysql_num_rows($resource)  获取查询结果集中的行数
int  mysql_num_fields($resource)  获取查询结果集中的字段数
```


