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






 
 
 


