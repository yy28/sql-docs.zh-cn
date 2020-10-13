---
title: 通过存储过程创建和访问 tempdb 表
description: TempDB 不支持通过原生编译存储过程创建和访问表。 使用内存优化表，或表类型和表变量。
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50db7b7594aeb244f5408cbf48efde7dd0fd703c
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867723"
---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>通过存储过程创建和访问 TempDB 中的表
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  不支持通过原生编译存储过程在 TempDB 中创建和访问表。 请改用具有 DURABILITY=SCHEMA_ONLY 的内存优化表或使用表类型和表变量。 

如需深入了解临时表和表变量场景下内存优化的信息，请参阅：[通过使用内存优化获得更快的时态表和表变量](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)。
  
  下面的示例演示如何将使用包含三列（ID、ProductID、Quantity）的临时表替换为使用 dbo.OrderQuantityByProduct 类型的表变量 \@OrderQuantityByProduct ：  
  
```sql  
CREATE TYPE dbo.OrderQuantityByProduct   
  AS TABLE   
   (id INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=100000),   
    ProductID INT NOT NULL,   
    Quantity INT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
GO  
CREATE PROCEDURE dbo.usp_OrderQuantityByProduct   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'ENGLISH'  
)  
  -- declare table variables for the list of orders   
  DECLARE @OrderQuantityByProduct dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @OrderQuantityByProduct SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>另请参阅  
 [本机编译的存储过程的迁移问题](./a-guide-to-query-processing-for-memory-optimized-tables.md)   
 [内存中 OLTP 不支持的 Transact-SQL 构造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
