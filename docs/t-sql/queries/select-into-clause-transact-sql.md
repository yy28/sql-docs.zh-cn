---
title: "INTO 子句 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTO_TSQL
- INSERT_INTO_TSQL
- INSERT INTO
- INTO
- INTO clause
- INTO_clause_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- copying data [SQL Server], into a new table
- INTO clause
- moving data, to a new table
- table creation [SQL Server], INTO clause
- SELECT INTO statement
- inserting rows
- clauses [SQL Server], INTO
- row additions [SQL Server], INTO clause
ms.assetid: b48d69e8-5a00-48bf-b2f3-19278a72dd88
caps.latest.revision: 63
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d8aa3c2ff42396114287f58b7d9d431d13de8a2f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="select---into-clause-transact-sql"></a>SELECT-INTO 子句 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  SELECT…INTO 在默认文件组中创建一个新表，并将来自查询的结果行插入该表中。 若要查看完整的选择语法，请参阅[选择 &#40;Transact SQL &#41;](../../t-sql/queries/select-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
[ INTO new_table ]
[ ON filegroup]
```  
  
## <a name="arguments"></a>参数  
 *new_table*  
 根据选择列表中的列和从数据源选择的行，指定要创建的新表名。  
 
  *文件组*
 
 指定将在其中创建新表的文件组的名称。 指定的文件组应数据库中存在其他 SQL Server 引擎将引发错误。 此选项仅支持开头[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]。
 
 格式*new_table*由评估选择列表中的表达式。 中的列*new_table*由 select 列表指定的顺序创建。 每个列中的*new_table*作为选择列表中的相应表达式具有相同名称、 数据类型，可为 null 性和值。 列的 IDENTITY 属性将被转移，但在“备注”部分的“使用标识列”中定义的情况除外。  
  
 在同一个实例上的另一个数据库中创建表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，指定*new_table*作为窗体中的完全限定名*database.schema.table_name*。  
  
 无法创建*new_table*在远程服务器; 但是，你可以填充到*new_table*从远程数据源。 若要创建*new_table*从远程源表，指定在窗体中使用由四部分构成的名称的源表*linked_server*。*目录*。*架构*。*对象*SELECT 语句的 FROM 子句中。 或者，可以使用[OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)函数或[OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md)要指定远程数据源的 FROM 子句中的函数。  
  
## <a name="data-types"></a>数据类型  
 FILESTREAM 属性不转移到新表。 复制和存储在与新的表中 FILESTREAM Blob **varbinary （max)** Blob。 不具有 FILESTREAM 属性， **varbinary （max)**数据类型具有 2 GB 的限制。 如果某个 FILESTREAM BLOB 超过该值，则会引发 7119 错误并停止该语句。  
  
 在选择现有标识列并将其插入到新表时，新列将继承 IDENTITY 属性，除非满足以下条件之一：  
  
-   SELECT 语句包含一个联接。  
  
-   多个 SELECT 语句由 UNION 联接。  
  
-   标识列在选择列表内多次列出。  
  
-   标识列是表达式的一部分。  
  
-   标识列来自远程数据源。  
  
如果这些条件中的一个为真，列将被创建为 NOT NULL 而不继承 IDENTITY 属性。 如果在新表中需要某一标识列，但此类列不可用，或者您需要不同于源标识列的种子或增量值，则使用 IDENTITY 函数在选择列表中定义该列。 请参阅下面的“示例”部分中的“使用 IDENTITY 函数创建标识列”。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 不能将表变量或表值参数指定为新表。  
  
 即使源表已进行分区，您也不能使用 SELECT…INTO 创建分区表。 SELECT...INTO 不使用源表的分区方案；而是在默认文件组中创建新表。 若要在分区表中插入行，必须先创建分区表，然后使用 INSERT INTO...SELECT FROM 语句。  
  
 源表中定义的索引、约束和触发器不会转移到新表中，也不能在 SELECT...INTO 语句中指定它们。 如果需要使用这些对象，您可以在执行 SELECT...INTO 语句后创建它们。  
  
 指定 ORDER BY 子句无法确保按指定顺序插入行。  
  
 当选择列表中包含稀疏列时，稀疏列属性不会转移到新表中的列。 如果需要在新表中使用该属性，请在执行 SELECT...INTO 语句后更改列定义以包含该属性。  
  
 当选择列表中包含计算列时，新表中的相应列并不是计算列。 新列中的值是在执行 SELECT...INTO 时计算的。  
  
## <a name="logging-behavior"></a>日志记录行为  
 SELECT...INTO 的日志记录量取决于数据库的有效恢复模式。 在简单恢复模式或大容量日志恢复模式下，大容量操作是最小日志记录操作。 与最小日志记录，使用 SELECT... INTO 语句可以是比创建表，然后填充具有 INSERT 语句的表更高效。 有关详细信息，请参阅 [事务日志 (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 在目标数据库中要求 CREATE TABLE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-table-by-specifying-columns-from-multiple-sources"></a>A. 通过指定来自多个源的列，创建一个表  
 下面的示例通过从与雇员或地址有关的各个表中选择七列创建 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的 `dbo.EmployeeAddresses` 表。  
  
```tsql  
SELECT c.FirstName, c.LastName, e.JobTitle, a.AddressLine1, a.City,   
    sp.Name AS [State/Province], a.PostalCode  
INTO dbo.EmployeeAddresses  
FROM Person.Person AS c  
    JOIN HumanResources.Employee AS e   
    ON e.BusinessEntityID = c.BusinessEntityID  
    JOIN Person.BusinessEntityAddress AS bea  
    ON e.BusinessEntityID = bea.BusinessEntityID  
    JOIN Person.Address AS a  
    ON bea.AddressID = a.AddressID  
    JOIN Person.StateProvince as sp   
    ON sp.StateProvinceID = a.StateProvinceID;  
GO  
```  
  
### <a name="b-inserting-rows-using-minimal-logging"></a>B. 使用最小日志记录插入行  
 下面的示例创建 `dbo.NewProducts` 表并从 `Production.Product` 表插入行。 此示例假定 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的恢复模式设置为 FULL。 若要确保最小方式记录，应在插入行之前将 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的恢复模式设置为 BULK_LOGGED，并在 SELECT...INTO 语句后重置为 FULL。 此过程确保 SELECT...INTO 语句在事务日志中占用最少的空间并且高效执行。  
  
```tsql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
  
SELECT * INTO dbo.NewProducts  
FROM Production.Product  
WHERE ListPrice > $25   
AND ListPrice < $100;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-creating-an-identity-column-using-the-identity-function"></a>C. 使用 IDENTITY 函数创建标识列  
 下面的示例使用 IDENTITY 函数在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的新表 `Person.USAddress` 中创建一个标识列。 这是必需的，因为定义该表的 SELECT 语句包含一个联接，而该联接导致 IDENTITY 属性不转移到新表。 请注意，在 IDENTITY 函数中指定的种子和增量值不同于源表 `AddressID` 的 `Person.Address` 列中的种子和增量值。  
  
```tsql  
-- Determine the IDENTITY status of the source column AddressID.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
  
-- Create a new table with columns from the existing table Person.Address. 
-- A new IDENTITY column is created by using the IDENTITY function.  
SELECT IDENTITY (int, 100, 5) AS AddressID,   
       a.AddressLine1, a.City, b.Name AS State, a.PostalCode  
INTO Person.USAddress   
FROM Person.Address AS a  
INNER JOIN Person.StateProvince AS b 
  ON a.StateProvinceID = b.StateProvinceID  
WHERE b.CountryRegionCode = N'US';   
  
-- Verify the IDENTITY status of the AddressID columns in both tables.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
```  
  
### <a name="d-creating-a-table-by-specifying-columns-from-a-remote-data-source"></a>D. 通过指定来自远程数据源的列，创建一个表  
 下面的示例演示从远程数据源在本地服务器上创建新表的三个方法。 该示例从创建指向远程数据源的链接开始。 链接的服务器名称，`MyLinkServer,`则在第一个选择的 FROM 子句中指定...到语句和 OPENQUERY 函数的第二个选择中...到语句。 第三个 SELECT...INTO 语句使用 OPENDATASOURCE 函数，该函数直接指定远程数据源，而非使用链接的服务器名称。  
  
 **适用于：** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```tsql
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_name\instance_name'.  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  

USE AdventureWorks2012;  
GO  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.Departments  
FROM MyLinkServer.AdventureWorks2012.HumanResources.Department  
GO  
-- Use the OPENQUERY function to access the remote data source.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenQuery  
FROM OPENQUERY(MyLinkServer, 'SELECT *  
               FROM AdventureWorks2012.HumanResources.Department');   
GO  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_name\instance_name.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenDataSource  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=server_name;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department;  
GO  
```  
  
### <a name="e-import-from-an-external-table-created-with--polybase"></a>E. 从外部表使用 PolyBase 创建导入  
 从 Hadoop 或 Azure 存储空间将数据导入到 SQL Server 进行永久存储。 使用`SELECT INTO`导入所引用的外部表进行 SQL Server 中的永久存储数据。 动态创建关系表，然后在第二步中创建基于该表的列存储索引。  
  
 **适用于：** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```tsql
-- Import data for car drivers into SQL Server to do more in-depth analysis.  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
```  
### <a name="f-creating-a-new-table-as-a-copy-of-another-table-and-loading-it-a-specified-filegroup"></a>F. 作为另一个表的副本创建新表并将其加载指定的文件组
以下示例 demostrates 作为另一个表的副本创建新表并将其加载到指定的文件组不同于用户的默认文件组。

 **适用于：**[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

```tsql
ALTER DATABASE [AdventureWorksDW2016] ADD FILEGROUP FG2;
ALTER DATABASE [AdventureWorksDW2016]
ADD FILE
(
NAME='FG2_Data',
FILENAME = '/var/opt/mssql/data/AdventureWorksDW2016_Data1.mdf'
)
TO FILEGROUP FG2;
GO
SELECT *  INTO [dbo].[FactResellerSalesXL] ON FG2 from [dbo].[FactResellerSales]
```
  
## <a name="see-also"></a>另请参阅  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [选择示例 &#40;Transact SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [标识 &#40;函数 &#41;&#40;Transact SQL &#41;](../../t-sql/functions/identity-function-transact-sql.md)  
  
  

