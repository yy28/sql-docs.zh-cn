---
title: 本机编译存储过程中的 CASE 表达式
ms.custom: seo-dt-2019
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2f82db01-da7e-4a7d-8bc0-48b245e6f768
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5c26cd8424000926030d37302606cece6a570668
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "74412645"
---
# <a name="implementing-a-case-expression-in-a-natively-compiled-stored-procedure"></a>在本机编译的存储过程中实现 CASE 表达式
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

适用对象：**和自** 开始的 SQL Server[!INCLUDE[ssSDSFull_md](../../includes/sssdsfull-md.md)][!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]

本机编译的 T-SQL 模块支持 CASE 表达式。 下面的示例演示了在查询中使用 CASE 表达式的方法。 

``` 
-- Query using a CASE expression in a natively compiled stored procedure.
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
   SELECT   
      SalesOrderID,   
      CASE (OnlineOrderFlag)   
      WHEN 1 THEN N'Order placed online by customer'  
      ELSE N'Order placed by sales person'  
      END  
   FROM Sales.SalesOrderHeader_inmem
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
``` 

适用对象：**和自** 开始的 SQL Server[!INCLUDE[ssSQL14-md](../../includes/ssSQL14-md.md)][!INCLUDE[ssSQL15-md](../../includes/ssSQL15-md.md)]

  本机编译的 T-SQL 模块不  支持 CASE 表达式。 以下示例演示一种在本机编译的存储过程中实现 CASE 表达式功能的方法。  
  
 代码示例使用表变量构造单个结果集。 这仅适合当于处理有限行数，因为它涉及到创建数据行的额外副本。  
  
 你应测试此解决方法的性能。  
  
```  
-- original query  
SELECT   
   SalesOrderID,   
   CASE (OnlineOrderFlag)   
   WHEN 1 THEN N'Order placed online by customer'  
   ELSE N'Order placed by sales person'  
   END  
FROM Sales.SalesOrderHeader_inmem  
  
--  workaround for CASE in natively compiled stored procedures  
--  use a table for the single resultset  
CREATE TYPE dbo.SOHOnlineOrderResult AS TABLE  
(  
   SalesOrderID uniqueidentifier not null index ix_SalesOrderID,  
     OrderFlag nvarchar(100) not null  
) with (memory_optimized=on)  
go  
  
-- natively compiled stored procedure that includes the query  
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  
      (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
  
   -- table variable for creating the single resultset  
   DECLARE @result dbo.SOHOnlineOrderResult  
  
   -- CASE OnlineOrderFlag=1  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed online by customer'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag=1  
  
   -- ELSE  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed by sales person'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag!=1  
  
   -- return single resultset  
   SELECT SalesOrderID, OrderFlag FROM @result  
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [本机编译的存储过程的迁移问题](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [内存中 OLTP 不支持的 Transact-SQL 构造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
