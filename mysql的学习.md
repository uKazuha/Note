# MySQL准备工作



## 一、安装与卸载

### 1.安装（zip安装包的方式）



第一步：解压ZIP（百度网盘有）

第二步：CMD，管理员方式运行，切换到bin目录下

第三步：安装mysql服务

```
mysqld -install [可以指定服务名称，默认为MySQL]

如果存在就先卸载
mysqld -remove
```

第四步：设置mysql配置文件，在最外层文件夹下创建my.ini

```
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8mb4
 
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8mb4
 
[mysqld]  # 服务端设置
# 设置3306端口
port=3306
# 重要，设置mysql的安装目录
basedir=D:\mysql-8.0.37-winx64
# 重要，设置mysql数据库的数据的存放目录
datadir=D:\mysql-8.0.37-winx64\data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8mb4
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

第五步：初始化mysql

```
mysqld --initialize --console
```

第六步：启动mysql服务

* 第一种命令启动

```
net start 服务名称
net stop 服务名称
```

第七步：登录

```
mysql -uroot -p

密码在mysqld --initialize --console执行后打印的信息里
```

第八步：修改密码

```mysql
ALTER USER '用户'@'localhost' IDENTIFIED BY '新密码';
```

配置环境变量：

```
setx PATH "%PATH;E:\mysql\mysql-8.4.4\bin"
```



我自己学习用的账号和密码都是root



## 二、图形化工具

一款连接mysql数据库的图形化工具：DBeaver，官网dbeaver.io，社区版完全够用，EXE方式，无脑下一步



## 三、一些必要操作

* 使用某个数据库

```sql
use 数据库名;
```

* 查看当前使用的数据库

```sql
select database();
```

* 列出所有数据库名称

```sql
show databases;
```

* 查看数据库的所有表名

```sql
show tables

或不切换库，直接指定库产看
show tables from 数据库名;
或
show tables in 数据库名;
```

* 创建数据库

```sql
create database 数据库名;
create database if not exists 数据库名;
```

* 创建表

```
create table if not exists 表名()
```



# 正式学习



## 二、检索数据

### 2.1 SELECT语句

```sql
检索单个列
select name from stu_info;
从stu_info表中查找名为name的一列数据

检索多个列
select name,age from stu_info;
多个列就加逗号隔开

检索所有列
select * from stu_info;
```

### 2.2 检索不同的值

```sql
select distinct age from stu_info;

distinct的作用是返回不同的值，如年龄有多个人都是20，那么结果只会有一个20的数据，否则就有很多行20
```



### 2.3 限制结果

* LIMIT：限制行数
* OFFSET：从哪一行开始

```sql
select name from stu_info
LIMIT 5
OFFSET 5;
即从第5行起的5行数据

--这是注释
```



## 三、排序检索数据

### 3.1 排序数据

* order by 

```sql
select age from stu_info
order by age;

按多个列排序
select name,age,id from stu_info
order by age,id;
先以age排，再以id排

按列的顺序排
select name,age,id from stu_info
order by 1,2;
数字代表字段的列数，从0开始
```

### 3.2 指定排序方向

* ASC升序
* DESC降序

```sql
默认升序
select age from stu_info
order by age;

指定降序
select age from stu_info
order by age DESC;
```



## 四、过滤数据

### 4.1 使用where子句

```sql
select name,age from stu_info
where age = 20;
查找年龄为20的信息
```

### 4.2 操作符

```
首先是一些数学符号：>,<,=,>=,<=,!=，!<,!>
其次是：is null，between ... and ...
```



## 五、高级数据过滤

### 5.1 组合where子句

* AND

```sql
select name,age,id from stu_info
where id = 2 and age < 20;
```

* OR

```sql
select name,age,id from stu_info
where id =2 or age < 20
```

AND的优先级更高，下面这种情况会导致，and 会先生效，结果为age<20且id=2的的信息，然后加上满足gender=男这一条件的信息

```sql
select name,gender,age,id from stu_info
where gender = "男" or age < 20 and id = 2;
```

我们可以加括号来解决

```sql
select name,gender,age,id from stu_info
where (gender = "男" or age < 20) and id = 2;
```



### 5.2 IN操作符

```sql
select name,age from stu_info
where age in (19,20,21);
```

* IN操作符一般比一组OR操作符执行的更快一些
* IN最大的优点是可以包含其他select语句

### 5.3 NOT操作符

仅一个作用，否定操作，放在关键字前，或后

```sql
create database if not exists [a];

select name,age from stu_info
where age not in (19,20,21);
```



## 六、使用通配符进行过滤

### 6.1 like操作符

1.通配符%

%可以匹配任意字符任意次数

注意：匹配不了null字段

```sql
select name from stu_info
where name like 'fish%';

-- 只能匹配文本字段，有时候一个文本字段容量有20位，但是实际只有10位，这个时候数据库会把后面10位用空格填充，即如下有时无法生效
select name from stu_info
where name like 'F%Y';	--本意是匹配以F开头，以Y结尾

-- 要修改成下面这样
select name from stu_info
where name like 'F%Y%';
```



2.通配符下划线_

只能匹配单个字符



3.通配符方括号[]

MySQL不支持，简单介绍用法

```sql
-- 匹配A或B开头的字段
select name from stu_info
where name like '[AB]%';

-- 用脱字符^或NOT执行相反操作
select name from stu_info
where name like '[^AB]%';
```

### 6.2 通配符使用的注意事项

* 其他操作符的优先级高于通配符
* 确实需要用时，不要在开头就使用