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

 
 
 


