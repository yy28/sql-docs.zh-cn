---
title: 演示：内存中 OLTP 的性能改进 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4858e4c35263ab3dd1d9fdcf55a2b136dd8eeaf2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050177"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>演示：内存中 OLTP 的性能改进
  此示例通过比较针对内存优化表和传统的基于磁盘的表运行完全相同的 TRANSACT-SQL 查询时响应时间上的差异，演示了使用内存中 OLTP 时的性能改进。 另外，还将创建本机编译存储过程（基于相同的查询），然后运行以演示你通常可在使用本机编译存储过程查询内存优化表时，获取最佳响应时间。 此示例只显示访问内存优化表数据时一个方面的性能改进；执行插入操作时的数据访问效率。 此示例是单线程的，未能利用内存中 OLTP 的并发利益。 使用并发的工作负荷将带来更高的性能提升。  
  
> [!NOTE]  
>  在 [SQL Server 2014 内存中 OLTP 示例](https://msftdbprodsamples.codeplex.com/releases/view/114491)中提供另一个用于演示内存优化表的示例。  
  
 为了完成本示例，你将执行以下操作：  
  
1.  创建一个名为 **imoltp** 的数据库并更改其文件详细信息以设置它，以便使用内存中 OLTP。  
  
2.  创建适用于我们的示例的数据库对象：三张表和一个本机编译存储过程。  
  
3.  运行不同的查询并显示每个查询的响应时间。  
  
 若要设置适用于我们的示例的 **imoltp** 数据库，请先创建一个空文件夹： **c:\imoltp_data**，然后运行以下代码：  
  
```sql  
USE master  
GO  
  
-- Create a new database.  
CREATE DATABASE imoltp  
GO  
  
-- Prepare the database for In-Memory OLTP by  
-- adding a memory-optimized filegroup to the database.  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_file_group  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
-- Add a file (to hold the memory-optimized data) to the new filegroup.  
ALTER DATABASE imoltp ADD FILE (name='imoltp_file', filename='c:\imoltp_data\imoltp_file')  
    TO FILEGROUP imoltp_file_group;  
GO  
  
```  
  
 接下来，运行以下代码创建基于磁盘的表、两 (2) 张内存优化表，以及将用于演示不同数据访问方法的本机编译存储过程：  
  
```sql  
USE imoltp  
GO  
  
-- If the tables or stored procedure already exist, drop them to start clean.  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'DiskBasedTable')  
   DROP TABLE [dbo].[DiskBasedTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'InMemTable')  
   DROP TABLE [dbo].[InMemTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'InMemTable2')  
   DROP TABLE [dbo].[InMemTable2]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'usp_InsertData')  
   DROP PROCEDURE [dbo].[usp_InsertData]  
GO  
  
-- Create a traditional disk-based table.  
CREATE TABLE [dbo].[DiskBasedTable] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
)  
GO  
  
-- Create a memory-optimized table.  
CREATE TABLE [dbo].[InMemTable] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a 2nd memory-optimized table.  
CREATE TABLE [dbo].[InMemTable2] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a natively-compiled stored procedure.  
CREATE PROCEDURE [dbo].[usp_InsertData]   
  @rowcount INT,  
  @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[inMemTable2](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
END  
GO  
  
```  
  
 设置已完成，我们可以执行查询，这些查询将显示响应时间来比较不同数据访问方法的性能。  
  
 若要完成示例，请多次运行下面的代码。 忽略第一次运行所返回的结果，第一次运行受到初始内存分配的负面影响。  
  
```sql  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Delete data from all tables to reset the example.  
DELETE FROM [dbo].[DiskBasedTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[inMemTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[InMemTable2]   
    WHERE [c1]>0  
GO  
  
-- Declare parameters for the test queries.  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
DECLARE @timems INT;  
DECLARE @starttime datetime2 = sysdatetime();  
  
-- Disk-based table queried with interpreted Transact-SQL.  
BEGIN TRAN  
  WHILE @I <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[DiskBasedTable](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (disk-based table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with interpreted Transact-SQL.  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN  
  WHILE @i <= @rowcount  
    BEGIN  
      INSERT INTO [dbo].[InMemTable](c1,c2) VALUES (@i, @c);  
      SET @i += 1;  
    END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with a natively-compiled stored procedure.  
SET @starttime = sysdatetime();  
  
EXEC usp_InsertData @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with natively-compiled stored procedure).';  
  
```  
  
 预期结果将提供实际响应时间，显示与针对传统的基于磁盘的表运行相同的工作负载相比，使用内存优化表和本机编译存储过程通常如何持续提供更快的响应时间。  
  
## <a name="see-also"></a>另请参阅  
 [用于演示内存中 OLTP 的 AdventureWorks 扩展](../../database-engine/extensions-to-adventureworks-to-demonstrate-in-memory-oltp.md)   
 [内存中 OLTP &#40;内存中优化&#41;](in-memory-oltp-in-memory-optimization.md)   
 [内存优化表](memory-optimized-tables.md)   
 [本机编译的存储过程](natively-compiled-stored-procedures.md)   
 [使用内存优化表的要求](requirements-for-using-memory-optimized-tables.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE 文件和文件组选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [创建过程和内存优化表](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
