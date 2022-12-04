## 1. SQL分类
- DDL（Data Definition Languages、数据定义语言），这些语句定义了不同的数据库、表、视图、索引等数据库对象，还可以用来创建、删除、修改数据库和数据表的结构
  - `CREATE`
  - `DROP`
  - `ALTER`
  - `RENAME`
- DML（Data Manipulation Language、数据操作语言），用于添加、删除、更新和查询数据库记录，并检查数据完整性
  - `INSERT`
  - `DELETE`
  - `UPDATE`
  - `SELECT`
- DCL（Data Control Language、数据控制语言），用于定义数据库、表、字段、用户的访问权限和安全级别
  - `GRANT`
  - `REVOKE`
  - `COMMIT`
  - `ROLLBACK`
  - `SAVEPOINT`

---

## 2. SQL语言的规则与规范
### 2.1 基本规则
- 每条命令以`;`结束
- 关于标点符号
  - 必须使用**英文状态**下的半角输入方式
  - 符串型和日期类型的数据可以使用单引号（`''`）表示
  - 列的别名，尽量使用双引号（`""`），而且不建议省略`as`
### 2.2 SQL大小写规范（建议遵守）
- MySQL在windows环境下是大小写不敏感
- MySQL在linux环境下是大小写敏感的
  - **数据库名、表名、表的别名、变量名是严格区分大小写的**
  - **关键字、函数名、列名（或字段名）、列的别名（字段的别名）是忽略大小写的**
- ==推荐采用统一的书写规范==：
    - 数据库名、表名、表别名、字段名、字段别名等都小写
    - SQL关键字、函数名、绑定变量等都大写
### 2.3 注释
- 单行注释：`#注释文字`
- 单行注释：`-- 注释文字` （--后面必须包含一个空格）
- 多行注释：`/* 注释文字 */`
### 2.4 数据的导入
在命令行客户端登陆mysql，使用`source`命令导入（一定要命令行cmd去执行，不能在navicat中写命令）
```sql
source d:\mysqldb.sql
```
## 3. 基本的SELECT语句

### 3.1 select ... from

#### 语法

```sql
select 字段1， 字段2 ... from 表名;
```

#### 选择全部列

```sql
select * from 表名;
```

- 一般情况下，除非需要使用表中所有的字段数据，==最好不要使用==通配符`*`。
- 通常会降低查询和所使用的应用程序的效率
- 通配符的优势是，当不知道所需要的列的名称时，可以通过它获取它们。

#### 选择特定的列

不同的列用逗号隔开，否则是别名

```sql
SELECT department_id, location_id
FROM departments;
```

### 3.2 列的别名

- 可以用`AS`，也可以省略
- 如果别名中间有空格，需要加双引号

```sql
SELECT last_name AS name, commission_pct comm
FROM employees;
```

### 3.3 去除重复行

在SELECT语句中使用关键字``DISTINCT`去除重复行

```sql
SELECT DISTINCT department_id
FROM employees;
```

特别注意：

- ==DISTINCT 需要放到所有列名的前面==

### 3.4 空值参与运算

记住：==所有运算符或列值遇到null值，运算结果都为null==，所以一般使用函数IFNULL来避免null参与运算

### 3.5 着重号

保证表中的字段、表名等没有和保留字、数据库系统或常用方法重复，如果冲突就需要使用着重号引起来

```sql
SELECT * FROM `ORDER`;
```

---



## 4. 显示表结构

```sql
DESCRIBE employees;
或
DESC employees;
```

![image-20221204190014023](D:\markdown\MySQL\0. MySQL基础\第三章-基本的SELECT语句.assets\image-20221204190014023.png)

- Field：表示字段名称。
- Type：表示字段类型，这里 barcode、goodsname 是文本型的，price 是整数类型的。
- Null：表示该列是否可以存储NULL值。
- Key：表示该列是否已编制索引。PRI表示该列是表主键的一部分；UNI表示该列是UNIQUE索引的一部分；MUL表示在列中某个给定值允许出现多次。
- Default：表示该列是否有默认值，如果有，那么值是多少。
- Extra：表示可以获取的与给定列有关的附加信息，例如AUTO_INCREMENT等。

---



## 5. 过滤数据

==where语句要放在from表后面==

```sql
SELECT 字段1,字段2
FROM 表名
WHERE 过滤条件
```

