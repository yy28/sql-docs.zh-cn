---
title: 内存优化表变量 |Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: bd102e95-53e2-4da6-9b8b-0e4f02d286d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 485f481819a9712f822f969c04d8e7050ad43bae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774405"
---
# <a name="memory-optimized-table-variables"></a>内存优化表变量
  除了内存优化表（用于高效的数据访问）和本机编译的存储过程（用于高效的查询处理和业务逻辑执行）之外，[!INCLUDE[hek_2](../includes/hek-2-md.md)] 还引入了第三种对象：内存优化表类型。 使用内存优化表类型创建的表变量是内存优化表变量。  
  
 与基于磁盘的表变量相比，内存优化表变量提供以下好处：  
  
-   变量仅存储于内存中。 数据访问更高效，因为内存优化表类型将相同的内存优化算法和数据结构用于内存优化表，特别是在本机编译的存储过程中使用变量时。  
  
-   对于内存优化表变量，不会占用 tempdb。 表变量存储于 tempdb 中，并且不会使用 tempdb 中的任何资源。  
  
 下面是内存优化表变量的典型使用方案：  
  
-   基于本机编译的存储过程中的多个查询，存储临时结果和创建单个结果集。  
  
-   将表值参数传递到本机编译的存储过程和解释型存储过程中。  
  
-   代替基于磁盘的表变量，并且在某些情况下代替对于存储过程而言是本地的 #temp 表。 这在系统中有许多 tempdb 争用的情况下特别有用。  
  
-   表变量可以用于模拟本机编译的存储过程中的游标，从而可帮助您解决本机编译的存储过程中的外围应用限制。  
  
 与内存优化表相似， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 为每个内存优化表类型都生成一个 DLL。 （创建内存优化表类型时，以及用于创建内存优化表变量时不编译即被调用。）此 DLL 包括用于访问索引的函数以及用于从表变量检索数据的函数。 当基于表类型声明一个内存优化表变量时，将在用户会话中创建与该表类型相对应的表和索引结构的实例。 然后，可采用与使用基于磁盘的表变量相同的方式使用该表变量。 您可以在表变量中插入、更新和删除行，并且可以在 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中使用变量。 还可以像表值参数 (TVP) 一样，将变量传递到本机编译的存储过程和解释型存储过程中。  
  
 下面的示例显示了基于 AdventureWorks 的内存中 OLTP 示例中的内存优化表类型 ([SQL Server 2014 内存中 OLTP 示例](https://msftdbprodsamples.codeplex.com/releases/view/114491))。  
  
```sql
CREATE TYPE Sales.SalesOrderDetailType_inmem
   AS TABLE
(
   OrderQty         smallint   NOT NULL,
   ProductID        int        NOT NULL,

   SpecialOfferID   int        NOT NULL
      INDEX  IX_SpecialOfferID  NONCLUSTERED,

   LocalID          int        NOT NULL,

   INDEX IX_ProductID HASH (ProductID)
      WITH ( BUCKET_COUNT = 8 )
)
WITH ( MEMORY_OPTIMIZED = ON );
```  
  
 该示例表明，内存优化的表类型的语法与基于磁盘的表类型相似，但具有以下不同：  
  
-   `MEMORY_OPTIMIZED=ON` 指示表类型是内存优化表。  
  
-   该类型必须有至少一个索引。 与内存优化表一样，可以使用哈希索引和非聚集索引。  
  
     对于哈希索引，Bucket 计数应该是预期唯一索引键数目的一倍到两倍。 有关详细信息，请参阅 [哈希索引确定正确的存储桶计数](../relational-databases/indexes/indexes.md)。  
  
-   针对内存优化表的数据类型和约束限制也适用于内存优化表类型。 例如，在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中支持默认约束，但不支持 CHECK 约束。  
  
 与内存优化表相似，内存优化表变量  
  
-   不支持并行计划。  
  
-   必须可容纳于内存中，并且不使用磁盘资源。  
  
 基于磁盘的表变量存在于 tempdb 中。 内存优化表变量存在于用户数据库中（但它们不占用存储空间并且不恢复）。  
  
 无法使用内联语法创建内存优化表。 与基于磁盘的表变量不同，您必须首先创建一个类型。  
  
## <a name="table-valued-parameters"></a>表值参数  
 下面的示例脚本显示如何将表变量声明为内存优化表类型 `Sales.SalesOrderDetailType_inmem`、将三行插入到该变量中以及将变量以 TVP 的形式传递到 `Sales.usp_InsertSalesOrder_inmem` 中。  
  
```sql  
DECLARE @od Sales.SalesOrderDetailType_inmem,  
  @SalesOrderID uniqueidentifier,  
  @DueDate datetime2 = SYSDATETIME()  
  
INSERT @od (LocalID, ProductID, OrderQty, SpecialOfferID) VALUES  
  (1, 888, 2, 1),  
  (2, 450, 13, 1),  
  (3, 841, 1, 1)  
  
EXEC Sales.usp_InsertSalesOrder_inmem  
  @SalesOrderID = @SalesOrderID,  
  @DueDate = @DueDate,  
 @OnlineOrderFlag = 1,  
  @SalesOrderDetails = @od  
```  
  
 内存优化表类型可用作针对存储过程表值参数 (TVP) 的类型，并且可与基于磁盘的表类型和 TVP 完全相同地由客户端引用。 因此，使用内存优化的 TVP 调用存储过程以及本机编译的存储过程在工作方式上与使用基于磁盘 TVP 调用解释型存储过程完全相同。  
  
## <a name="temp-table-replacement"></a>#temp 表替换  
 下面的示例显示内存优化表类型和表变量，用来代替对于存储过程而言处于本地的 #temp 表。  
  
```sql  
-- Using SQL procedure and temp table  
CREATE TABLE #tempTable (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
  
CREATE PROCEDURE sqlProc  
AS  
BEGIN  
  TRUNCATE TABLE #tempTable  
  
  INSERT #tempTable VALUES (1)  
  INSERT #tempTable VALUES (2)  
  INSERT #tempTable VALUES (3)  
  SELECT * FROM #tempTable  
END  
GO  
  
-- Using natively compiled stored procedure and table variable  
CREATE TYPE TT AS TABLE (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
GO  
  
CREATE PROCEDURE NCSPProc  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @tableVariable TT  
  INSERT @tableVariable VALUES (1)  
  INSERT @tableVariable VALUES (2)  
  INSERT @tableVariable VALUES (3)  
  SELECT c FROM @tableVariable  
END  
GO  
```  
  
## <a name="creating-a-single-result-set"></a>创建单个结果集  
 下面的示例显示如何基于本机编译的存储过程中的多个查询，存储临时结果和创建单个结果集。 该示例计算并集 `SELECT c1 FROM dbo.t1 UNION SELECT c1 FROM dbo.t2`。  
  
```sql  
CREATE DATABASE hk  
GO  
ALTER DATABASE hk ADD FILEGROUP hk_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hk ADD FILE( NAME = 'hk_mod' , FILENAME = 'c:\data\hk_mod') TO FILEGROUP hk_mod;  
  
USE hk  
GO  
  
CREATE TYPE tab1 AS TABLE (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON)  
  
CREATE TABLE dbo.t1 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
CREATE TABLE dbo.t2 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
  
INSERT INTO dbo.t1 VALUES (1), (2)  
INSERT INTO dbo.t2 VALUES (3), (4)  
GO  
  
CREATE PROCEDURE dbo.p1  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS  
  BEGIN ATOMIC WITH ( TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english' )  
  
    DECLARE @t dbo.tab1  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t1;  
  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t2;  
  
    SELECT c1 FROM @t;  
  END  
GO  
  
EXEC dbo.p1  
GO  
```  
  
## <a name="memory-consumption-for-table-variables"></a>表变量的内存使用情况  
 表变量的内存使用情况类似于内存优化表，只是在非聚集索引上有所不同。 如果将多个行插入带有非聚集索引的内存优化表变量，并且索引键很大，则这些表变量将使用不成比例的内存量。 大型表变量上的非聚集索引需要的内存按比例高于插入表中的相同数量行的非聚集索引所需要的内存（索引页面中内存更多）。  
  
 表变量使用的内存来自数据库的资源调控器资源池。  
  
 与内存优化表不同，表变量使用的内存（包括删除的行）在表变量超出作用域时将被释放。  
  
 内存将作为数据库的单一 PGPOOL 内存消耗者的一部分加以考虑。  
  
## <a name="see-also"></a>请参阅  
 [对内存中 OLTP 的 Transact-SQL 支持](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
