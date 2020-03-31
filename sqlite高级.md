- **SQLite PRAGMA**  
在sqlite环境内控制各种环境变量和状态标志。  
语法：PRAGMA pragma_name;  
设置新值：PRAGMA pragma_name = value;  
1. auto_vacuum Pragma  
auto_vacuum Pragma获取或设置auto-vacuum模式。  
语法：PRAGMA [database.]auto_vacuum;  
     PRAGMA [database.]auto_vacuum = mode;  
pragma值：0或NONE:禁用Auto-vacuum。  
         1或FULL：启用Auto-vacuum,是全自动的。  
         2或INCREMENTAL：启用Auto-vacuum，但是必须手动激活。  
2.cache_size Pragma  
 可获取或暂时设置在内存中页面缓存的最大尺寸。  
语法：PRAGMA [database.]cache_size;  
     PRAGMA [database.]cache_size = pages;  
更多pragma详情请看：https://www.runoob.com/sqlite/sqlite-pragma.html  
- **约束**  
常用约束：NOT NULL，DEFAULT(该列没有指定值时，提供默认值),UNIQUE,PRIMARY KEY,CHECK(确保该列的值满足某一条件)  
实例：DEFAULT 50000.00，CHECK(SALARY>0)  
- **JOIN**  
类型：  
交叉连接-CROSS JOIN (返回两张表所有的行)   
内连接-INNER JOIN  
外连接-OUTER JOIN  
为了避免冗余，并保持较短的措辞，可以使用 USING 表达式声明外连接（OUTER JOIN）条件。  
 SQLite 只支持 左外连接（LEFT OUTER JOIN)  
 -**UNION子句**  
 用于合并两个或多个 SELECT 语句的结果，不返回任何重复的行，每个SELECT被选择的列数必须是相同的。
 语法：
 ```sqlite
 SELECT column1 [, column2 ]
FROM table1 [, table2 ]
[WHERE condition]

UNION

SELECT column1 [, column2 ]
FROM table1 [, table2 ]
[WHERE condition]
 ```  
- **UNION ALL子句**  
UNION ALL 运算符用于结合两个 SELECT 语句的结果，包括重复行。 
语法：  
```sqlite
SELECT column1 [, column2 ]
FROM table1 [, table2 ]
[WHERE condition]

UNION ALL

SELECT column1 [, column2 ]
FROM table1 [, table2 ]
[WHERE condition]
```  
- **NULL值**  
实例：UPDATE COMPANY SET ADDRESS = NULL, SALARY = NULL where ID IN(6,7);  
 WHERE SALARY IS NOT NULL;  
- **SQLITE别名**  
暂时把表或列重命名为另一个名字，这被称为别名。  
语法：  
```
SELECT column1,column2... FROM table_name AS alias_name  
SELECT colunm1 AS alias_name FROM table_name  
```  
- **SQLITE 触发器（Trigger)**  
SQLite 触发器（Trigger）是数据库的回调函数，它会在指定的数据库事件发生时自动执行/调用。以下是关于 SQLite 的触发器（Trigger）的要点：  
1.SQLite 的触发器（Trigger）可以指定在特定的数据库表发生 DELETE、INSERT 或 UPDATE 时触发，或在一个或多个指定表的列发生更新时触发。  
2.SQLite 只支持 FOR EACH ROW 触发器（Trigger），没有 FOR EACH STATEMENT 触发器（Trigger）。因此，明确指定 FOR EACH ROW 是可选的。  
3.WHEN 子句和触发器（Trigger）动作可能访问使用表单 NEW.column-name 和 OLD.column-name 的引用插入、删除或更新的行元素，其中 column-name 是从与触发器关联的表的列的名称。  
4.如果提供 WHEN 子句，则只针对 WHEN 子句为真的指定行执行 SQL 语句。如果没有提供 WHEN 子句，则针对所有行执行 SQL 语句。  
5.BEFORE 或 AFTER 关键字决定何时执行触发器动作，决定是在关联行的插入、修改或删除之前或者之后执行触发器动作。  
6.当触发器相关联的表删除时，自动删除触发器（Trigger）。  
7.要修改的表必须存在于同一数据库中，作为触发器被附加的表或视图，且必须只使用 tablename，而不是 database.tablename。  
8.一个特殊的 SQL 函数 RAISE() 可用于触发器程序内抛出异常。  
**语法：**  
```
REATE  TRIGGER trigger_name [BEFORE|AFTER] [UPDATE] OF column_name 
ON table_name
[FOR EACH ROW]
BEGIN
 -- 触发器逻辑....
END;
```
**实例：**
```
sqlite> CREATE TRIGGER audit_log AFTER INSERT 
ON COMPANY
BEGIN
   INSERT INTO AUDIT(EMP_ID, ENTRY_DATE) VALUES (new.ID, datetime('now'));
END;
``` 
从sqlite_master表中列出所有触发器：
```
sqlite> SELECT name FROM sqlite_master
WHERE type = 'trigger';
```  
- **SQLITE索引(Index)**  
索引有助于加快 SELECT 查询和 WHERE 子句，但它会减慢使用 UPDATE 和 INSERT 语句时的数据输入。索引可以创建或删除，但不会影响数据。  
语法：  
CREATE INDEX index_name ON table_name;  
基于某一列的：  
CREATE INDEX index_name ON table_name(column_name);  
唯一索引：  
CREATE UNIQUE INDEX index_name ON table_name(column_name);  
组合索引：  
CREATE INDEX index_name ON table_name(column1,column2);  
**要避免使用索引的情况有：**  
1.索引不应该使用在较小的表上。  
2.索引不应该使用在有频繁的大批量的更新或插入操作的表上。  
3.索引不应该使用在含有大量的 NULL 值的列上。  
4.索引不应该使用在频繁操作的列上。 
- **INDEXED BY**  
用于子句规定按照索引来查找表中  
index-name不存在或不能用于查询，SQLite语句的准备失败  
其他语句还有：NOT INDEXED  
**语法：**  
```
SELECT|DELETE|UPDATE column1, column2...
FROM table_name
INDEXED BY (index_name)
WHERE (CONDITION);
```  
- **ALTER命令**  
 ALTER TABLE 命令不通过执行一个完整的转储和数据的重载来修改已有的表。  
在 SQLite 中，除了重命名表和在已有的表中添加列，ALTER TABLE 命令不支持其他操作。  
**语法**  
```
修改表名：
ALTER TABLE database_name.table_name RENAME TO new_table_name;
添加列：
ALTER TABLE database_name.table_name ADD COLUMN column_def...;
```  
- **没有TRUNCATE TABLE**  
在 SQLite 中，并没有 TRUNCATE TABLE 命令，但可以使用 SQLite 的 DELETE 命令从已有的表中删除全部的数据。  
```
递增归零：
DELETE FROM sqlite_sequence WHERE name = 'table_name';
```  
- **视图View**  
1)视图（View）只不过是通过相关的名称存储在数据库中的一个 SQLite 语句。视图（View）实际上是一个以预定义的 SQLite 查询形式存在的表的组合。  
2)视图（View）是一种虚表，允许用户实现以下几点：  
1.用户或用户组查找结构数据的方式更自然或直观。  
2.限制数据访问，用户只能看到有限的数据，而不是完整的表。  
3.汇总各种表中的数据，用于生成报告。
SQLite视图是只读的  
语法：  
```
创建视图：
CREATE [TEMP | TEMPORARY(在临时数据库中)] VIEW view_name AS
SELECT column1, column2.....
FROM table_name
WHERE [condition];（可以包含多个表）
删除视图：
DROP VIEW view_name;
```  
  
---------------------------------------  
- **事务TRANSACTION**  
1.**定义**  
事务（Transaction）是一个对数据库执行工作单元。事务（Transaction）是以逻辑顺序完成的工作单位或序列，可以是由用户手动操作完成，也可以是由某种数据库程序自动完成。  
事务（Transaction）是指一个或多个更改数据库的扩展。例如，如果您正在创建一个记录或者更新一个记录或者从表中删除一个记录，那么您正在该表上执行事务。重要的是要控制事务以确保数据的完整性和处理数据库错误。  

-------------------------------------------------
2.**事务的属性** 
通常根据首字母缩写为 ACID：  
1）**原子性（Atomicity）** ：确保工作单位内的所有操作都成功完成，否则，事务会在出现故障时终止，之前的操作也会回滚到以前的状态。  
2）**一致性（Consistency)** ：确保数据库在成功提交的事务上正确地改变状态。  
3）**隔离性（Isolation）**：使事务操作相互独立和透明。  
4）**持久性（Durability）**：确保已提交事务的结果或效果在系统发生故障的情况下仍然存在。 

--------------------------------------------------------
3.**BEGIN TRANSACTION命令**  
BEGIN TRANSACTION/BEGIN：开始事务处理。  
4.**COMMIT命令**  
COMMIT/END TRANSACTION：保存更改，或者可以使用 END TRANSACTION 命令。  
5.**ROLLBACK命令**  
ROLLBACK：回滚所做的更改。  
6.**例子**  
```
BEGIN;
DELETE FROM COMPANY WHERE AGE = 25;
ROLLBACK;
(再次查询表无变化) 
BEGIN;
DELETE FROM COMPANY WHERE AGE = 25;
COMMIT;
(再次查询表年龄25岁记录被删除)
```  

- **SQLite子查询**  
子查询可以与 SELECT、INSERT、UPDATE 和 DELETE 语句一起使用，可伴随着使用运算符如 =、<、>、>=、<=、IN、BETWEEN 等。
**子查询的几个规则**  
- 子查询必须用括号括起来。  
- 子查询在 SELECT 子句中只能有一个列，除非在主查询中有多列，与子查询的所选列进行比较。  
- ORDER BY 不能用在子查询中，虽然主查询可以使用 ORDER BY。可以在子查询中使用 GROUP BY，功能与 ORDER BY 相同。  
- 子查询返回多于一行，只能与多值运算符一起使用，如 IN 运算符。  
- BETWEEN 运算符不能与子查询一起使用，但是，BETWEEN 可在子查询内使用。  
**例子**  
``` 
在SELECT语句中：
SELECT * FROM COMPANY WHERE ID IN 
(SELECT ID FROM COMPANY WHERE SALARY > 45000) ;
在INSERT语句中：
INSERT INTO COMPANY_BKP SELECT * FROM COMPANY WHERE ID IN 
(SELECT ID FROM COMPANY) ;
在UPDATE语句中:
UPDATE COMPANY SET SALARY = SALARY * 0.50 WHERE AGE IN 
(SELECT AGE FROM COMPANY_BKP WHERE AGE >= 27 );
在DELETE语句中：
DELETE FROM COMPANY WHERE AGE IN 
(SELECT AGE FROM COMPANY_BKP WHERE AGE > 27 );
```  
- **autoincrement(自动递增)**  
SQLite 的 AUTOINCREMENT 是一个关键字，用于表中的字段值自动递增。我们可以在创建表时在特定的列名称上使用 AUTOINCREMENT 关键字实现该字段值的自动增加。  
关键字 AUTOINCREMENT 只能用于整型（INTEGER）字段。  
**例子** 
```
CREATE TABLE COMPANY(
ID INTEGER PRIMARY KEY   AUTOINCREMENT,  
   NAME           TEXT      NOT NULL,  
   AGE            INT       NOT NULL,  
   ADDRESS        CHAR(50),  
   SALARY         REAL  
); 
```  
- **SQLite注入**  
如果您的站点允许用户通过网页输入，并将输入内容插入到 SQLite 数据库中，这个时候您就面临着一个被称为 SQL 注入的安全问题。  
注入通常在请求用户输入时发生，比如需要用户输入姓名，但用户却输入了一个 SQLite 语句，而这语句就会在不知不觉中在数据库上运行。  
- **Explain(解释)**  
在 SQLite 语句之前，可以使用 "EXPLAIN" 关键字或 "EXPLAIN QUERY PLAN" 短语，用于描述表的细节。 1)来自 EXPLAIN 和 EXPLAIN QUERY PLAN 的输出只用于交互式分析和排除故障。  
2)输出格式的细节可能会随着 SQLite 版本的不同而有所变化。  
3)应用程序不应该使用 EXPLAIN 或 EXPLAIN QUERY PLAN，因为其确切的行为是可变的且只有部分会被记录。  
**例子**  
```
EXPLAIN SELECT *  FROM COMPANY  WHERE Salary &gt= 20000;
EXPLAIN QUERY PLAN SELECT * FROM COMPANY WHERE Salary &gt= 20000;
```  
- **Vacuum**  
VACUUM 命令通过复制主数据库中的内容到一个临时数据库文件，然后清空主数据库，并从副本中重新载入原始的数据库文件。这消除了空闲页，把表中的数据排列为连续的，另外会清理数据库文件结构。  
详情：https://www.runoob.com/sqlite/sqlite-vacuum.html  
- **日期&时间**  
基本：https://www.runoob.com/sqlite/sqlite-date-time.html  

















 
 
 


