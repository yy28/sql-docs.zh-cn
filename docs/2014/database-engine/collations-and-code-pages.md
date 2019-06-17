---
title: 排序规则和代码页 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c626dcac-0474-432d-acc0-cfa643345372
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1969a3e30b31a21c380559a3e8898f87eb8848b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786732"
---
# <a name="collations-and-code-pages"></a>排序规则和代码页
  [!INCLUDE[hek_2](../includes/hek-2-md.md)] 对于内存优化表中的 (var)char 列的支持代码页，以及在索引和本机编译存储过程中使用的支持的排序规则方面存在限制。  
  
 (var)char 值的代码页决定着字符与存储在表中的字节表示之间的映射。 例如，使用 Windows Latin 1 代码页（1252；[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的默认代码页）时，字符 'a' 对应字节 0x61。  
  
 (var)char 值的代码页由与该值关联的排序规则决定。 例如，排序规则 SQL_Latin1_General_CP1_CI_AS 的关联代码页为 1252。  
  
 值的排序规则继承自数据库的排序规则，也可使用 COLLATE 关键字显式指定。 如果数据库包含内存优化的表或本机编译的存储过程，则无法更改数据库排序规则。 下面的示例设置数据库的排序规则，并创建一个包含采用不同排序规则的列的表。 该数据库使用 Latin 不区分大小写的排序规则。  
  
 如果字符串列采用 BIN2 排序规则，则只能在该列上创建索引。 LastName 变量采用 BIN2 排序规则。 FirstName 采用数据库默认排序规则，即 CI_AS（不区分大小写，区分重音）。  
  
> [!IMPORTANT]  
>  无法对不使用 BIN2 排序规则的索引字符串列使用 order by 或 group by。  
  
```sql  
CREATE DATABASE IMOLTP  
  
ALTER DATABASE IMOLTP ADD FILEGROUP IMOLTP_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP ADD FILE( NAME = 'IMOLTP_mod' , FILENAME = 'c:\data\IMOLTP_mod') TO FILEGROUP IMOLTP_mod;  
--GO  
  
--  set the database collations  
ALTER DATABASE IMOLTP COLLATE Latin1_General_100_CI_AS  
GO  
  
--  
USE IMOLTP   
GO  
  
-- create a table with collation  
CREATE TABLE Employees (  
  EmployeeID int NOT NULL ,   
  LastName nvarchar(20) COLLATE Latin1_General_100_BIN2 NOT NULL INDEX IX_LastName NONCLUSTERED,   
  FirstName nvarchar(10) NOT NULL ,  
  CONSTRAINT PK_Employees PRIMARY KEY NONCLUSTERED HASH(EmployeeID)  WITH (BUCKET_COUNT=1024)  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_AND_DATA)  
GO  
```  
  
 下述限制适用于内存优化的表和本机编译的存储过程：  
  
-   内存优化表中的 (var)char 列必须使用代码页 1252 排序规则。 此限制不适用于 n(var)char 列。 下列代码检索所有 1252 排序规则：  
  
    ```sql  
    -- all supported collations for (var)char columns in memory-optimized tables  
    select * from sys.fn_helpcollations()  
    where collationproperty(name, 'codepage') = 1252;  
    ```  
  
     如果需要存储非拉丁字符，请使用 n(var)char 列。  
  
-   (n)(var)char 列的索引只能以 BIN2 排序规则指定（参阅第一个示例）。 下面的查询检索所有支持的 BIN2 排序规则：  
  
    ```sql  
    -- all supported collations for indexes on memory-optimized tables and   
    -- comparison/sorting in natively compiled stored procedures  
    select * from sys.fn_helpcollations() where name like '%BIN2'  
    ```  
  
     如果通过解释的 [!INCLUDE[tsql](../includes/tsql-md.md)] 访问表，则可借助 `COLLATE` 关键字通过表达式或排序操作更改排序规则。 相关示范见上一个示例。  
  
-   如果数据库排序规则不是代码页 1252 排序规则，则本机编译的存储过程不能使用 (var)char 类型的参数、局部变量或字符串常量。  
  
-   本机编译存储过程中的所有表达式和排序操作都必须使用 BIN2 排序规则。 也就是说，所有比较和排序操作都基于字符（二进制表）的 Unicode 码位。 例如，所有排序操作均区分大小写（“Z”位于“a”之前）。 如有必要，可使用解释的 [!INCLUDE[tsql](../includes/tsql-md.md)] 进行不区分大小写的排序和比较。  
  
-   本机编译的存储过程内部不支持 UTF-16 数据截断。 这意味着该 n (var) char (*n*) 的值无法转换为类型 n (var) char (*我*)，如果*我* < *n*，如果排序规则具有 _SC 属性。 例如，不支持以下操作：  
  
    ```sql  
    -- column definition using an _SC collation  
     c2 nvarchar(200) collate Latin1_General_100_CS_AS_SC not null   
    -- assignment to a smaller variable, requiring truncation  
     declare @c2 nvarchar(100) = '';  
     select @c2 = c2  
    ```  
  
     在本机编译的存储过程中不支持字符串操作函数，例如 LEN、SUBSTRING、LTRIM 和具有 UTF-16 数据的 RTRIM。 不能将这些字符串操作函数用于具有 _SC 排序规则的 n(var)char 值。  
  
     使用足够大的类型声明变量以避免截断。  
  
 下面的示例演示了内存中 OLTP 中排序规则限制的一些影响和解决方法。 该示例使用上面指定的 Employees 表。 此示例列出所有雇员。 注意，对于 LastName，出于二进制排序规则的原因，大写名称将排在小写名称之前。 因此，'Thomas' 排在 'nolan' 之前（因为大写字符的码位在前）。 FirstName 拥有不区分大小写的排序规则。 因此，字符以其在字母表中的位置而非该字符的码位进行排序。  
  
```sql  
-- insert a number of values  
INSERT Employees VALUES (1,'thomas', 'john')  
INSERT Employees VALUES (2,'Thomas', 'rupert')  
INSERT Employees VALUES (3,'Thomas', 'Jack')  
INSERT Employees VALUES (4,'Thomas', 'annie')  
INSERT Employees VALUES (5,'nolan', 'John')  
GO  
  
-- ===========  
SELECT EmployeeID, LastName, FirstName FROM Employees  
ORDER BY LastName, FirstName  
GO  
  
-- ===========  
-- specify collation: sorting uses case-insensitive collation, thus 'nolan' comes before 'Thomas'  
SELECT * FROM Employees  
ORDER BY LastName COLLATE Latin1_General_100_CI_AS, FirstName  
GO  
  
-- ===========  
-- retrieve employee by Name  
-- must use BIN2 collation for comparison in natively compiled stored procedures  
CREATE PROCEDURE usp_EmployeeByName @LastName nvarchar(20), @FirstName nvarchar(10)  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = N'us_english'  
)  
  SELECT EmployeeID, LastName, FirstName FROM dbo.Employees  
  WHERE   
    LastName = @LastName AND  
    FirstName COLLATE Latin1_General_100_BIN2 = @FirstName  
  
END  
GO  
  
-- this does not return any rows, as EmployeeID 1 has first name 'john', which is not equal to 'John' in a binary collation  
EXEC usp_EmployeeByName 'thomas', 'John'  
  
-- this retrieves EmployeeID 1  
EXEC usp_EmployeeByName 'thomas', 'john'  
```  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
